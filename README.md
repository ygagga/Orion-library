-- Carregar Orion Library
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Orion/main/source"))()
local Window = OrionLib:MakeWindow({
    Name = "Brookhaven RP 🏡 (Troll Hub 🤡)",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TrollHub",
    IntroEnabled = false
})

-- Criando as abas
local TrollTab = Window:MakeTab({ Name = "🤡 Troll", Icon = "rbxassetid://4483345998", PremiumOnly = false })
local MusicTab = Window:MakeTab({ Name = "🎶 Música", Icon = "rbxassetid://4483345998", PremiumOnly = false })
local HacksTab = Window:MakeTab({ Name = "⚡ Hacks", Icon = "rbxassetid://4483345998", PremiumOnly = false })
local ScriptsTab = Window:MakeTab({ Name = "🧑‍💻 Scripts", Icon = "rbxassetid://4483345998", PremiumOnly = false })
local AboutTab = Window:MakeTab({ Name = "ℹ️ Sobre", Icon = "rbxassetid://4483345998", PremiumOnly = false })

-- Variáveis para Troll
local selectedPlayer = ""
local isSpectating = false

TrollTab:AddTextbox({
    Name = "Nome do Jogador",
    Default = "",
    TextDisappear = false,
    Callback = function(value)
        selectedPlayer = value
    end
})

TrollTab:AddButton({
    Name = "Teleportar Todos 🏃‍♂️",
    Callback = function()
        local players = game:GetService("Players")
        local localPlayer = players.LocalPlayer
        local localHumanoidRootPart = localPlayer.Character and localPlayer.Character:FindFirstChild("HumanoidRootPart")

        if localHumanoidRootPart then
            for _, targetPlayer in pairs(players:GetPlayers()) do
                if targetPlayer ~= localPlayer and targetPlayer.Character then
                    local targetRoot = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
                    if targetRoot then
                        targetRoot.CFrame = localHumanoidRootPart.CFrame
                    end
                end
            end
        end
    end
})

TrollTab:AddButton({
    Name = "Espectar 👀",
    Callback = function()
        if selectedPlayer ~= "" then
            local players = game:GetService("Players")
            local targetPlayer = players:FindFirstChild(selectedPlayer)

            if targetPlayer and targetPlayer.Character then
                local camera = game.Workspace.CurrentCamera
                camera.CameraSubject = targetPlayer.Character:FindFirstChildOfClass("Humanoid")
                isSpectating = true
            end
        end
    end
})

TrollTab:AddButton({
    Name = "Despectar 🚶‍♂️",
    Callback = function()
        if isSpectating then
            local players = game:GetService("Players")
            local localPlayer = players.LocalPlayer
            local camera = game.Workspace.CurrentCamera
            camera.CameraSubject = localPlayer.Character:FindFirstChildOfClass("Humanoid")
            isSpectating = false
        end
    end
})

-- Música
local musicId = ""
local loopMusic = false
local musicPlaying = nil

MusicTab:AddTextbox({
    Name = "ID da Música",
    Default = "",
    TextDisappear = false,
    Callback = function(value)
        musicId = value
    end
})

MusicTab:AddToggle({
    Name = "Loop",
    Default = false,
    Callback = function(value)
        loopMusic = value
    end
})

MusicTab:AddButton({
    Name = "Reproduzir Música 🎶",
    Callback = function()
        if musicId ~= "" then
            if musicPlaying then
                musicPlaying:Stop()
                musicPlaying:Destroy()
            end

            musicPlaying = Instance.new("Sound")
            musicPlaying.SoundId = "rbxassetid://" .. musicId
            musicPlaying.Looped = loopMusic
            musicPlaying.Volume = 1
            musicPlaying.Parent = game:GetService("Workspace")
            musicPlaying:Play()
        end
    end
})

-- Hacks
HacksTab:AddButton({
    Name = "Ativar Super Velocidade ⚡",
    Callback = function()
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100
    end
})

HacksTab:AddButton({
    Name = "Desativar Velocidade ❌",
    Callback = function()
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
    end
})

HacksTab:AddButton({
    Name = "Ativar Pulo Infinito 🦘",
    Callback = function()
        game:GetService("UserInputService").JumpRequest:Connect(function()
            game.Players.LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        end)
    end
})

HacksTab:AddButton({
    Name = "Desativar Pulo Infinito ❌",
    Callback = function()
        game:GetService("UserInputService").JumpRequest:Disconnect()
    end
})

HacksTab:AddButton({
    Name = "Ativar Atravessar Paredes 🚪",
    Callback = function()
        local player = game.Players.LocalPlayer
        local character = player.Character
        for _, part in pairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
            end
        end
    end
})

HacksTab:AddButton({
    Name = "Desativar Atravessar Paredes ❌",
    Callback = function()
        local player = game.Players.LocalPlayer
        local character = player.Character
        for _, part in pairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = true
            end
        end
    end
})

-- Scripts
ScriptsTab:AddButton({
    Name = "Fly Script ✈️",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()
    end
})

ScriptsTab:AddButton({
    Name = "RAEL Hub 🔧",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Laelmano24/Rael-Hub/main/main.txt"))()
    end
})

ScriptsTab:AddButton({
    Name = "Sander X 🛸",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/sXPiterXs1111/Sanderxv3.30/main/sanderx3.30"))()
    end
})

-- Sobre
AboutTab:AddParagraph("Criado por Shelby, user Discord: snobodj")
AboutTab:AddParagraph("Troll Hub para bagunçar no Brookhaven RP!")
AboutTab:AddParagraph("Aproveite e divirta-se, mas sem exagerar! 😆")

-- Finalizar a UI
OrionLib:Init()
