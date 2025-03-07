-- Carrega a Orion Library
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Orion/main/source"))()

-- Criando a interface principal
local Window = OrionLib:MakeWindow({
    Name = "Brookhaven RP 🏡 (Troll Hub 🤡)",
    HidePremium = false,
    SaveConfig = false,
    ConfigFolder = "TrollHub"
})

-- Criando as abas
local TrollTab = Window:MakeTab({
    Name = "🤡 Troll",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local MusicTab = Window:MakeTab({
    Name = "🎶 Música",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local HacksTab = Window:MakeTab({
    Name = "⚡ Hacks",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local ScriptsTab = Window:MakeTab({
    Name = "🧑‍💻 Scripts",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local AboutTab = Window:MakeTab({
    Name = "ℹ️ Sobre",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Variável do jogador selecionado
local selectedPlayer = ""

-- Campo de entrada de jogador
TrollTab:AddTextbox({
    Name = "Nome do Jogador",
    Default = "",
    TextDisappear = true,
    Callback = function(value)
        selectedPlayer = value
    end
})

-- Botão de espectar jogador
TrollTab:AddButton({
    Name = "Espectar 👀",
    Callback = function()
        if selectedPlayer ~= "" then
            local players = game:GetService("Players")
            local targetPlayer = players:FindFirstChild(selectedPlayer)
            if targetPlayer and targetPlayer.Character then
                game.Workspace.CurrentCamera.CameraSubject = targetPlayer.Character:FindFirstChildOfClass("Humanoid")
            end
        end
    end
})

-- Botão de matar jogador
TrollTab:AddButton({
    Name = "Matar Jogador ☠️",
    Callback = function()
        if selectedPlayer ~= "" then
            local target = game.Players:FindFirstChild(selectedPlayer)
            if target and target.Character and target.Character:FindFirstChild("Humanoid") then
                target.Character.Humanoid.Health = 0
            end
        end
    end
})

-- Botão de teleportar jogador
TrollTab:AddButton({
    Name = "Teleportar 🔀",
    Callback = function()
        if selectedPlayer ~= "" then
            local localPlayer = game.Players.LocalPlayer
            local target = game.Players:FindFirstChild(selectedPlayer)
            if target and target.Character and localPlayer.Character then
                local targetHRP = target.Character:FindFirstChild("HumanoidRootPart")
                local myHRP = localPlayer.Character:FindFirstChild("HumanoidRootPart")
                if targetHRP and myHRP then
                    targetHRP.CFrame = myHRP.CFrame
                end
            end
        end
    end
})

-- 📌 **SEÇÃO DE MÚSICA**
local musicId = ""
MusicTab:AddTextbox({
    Name = "ID da Música",
    Default = "",
    TextDisappear = true,
    Callback = function(value)
        musicId = value
    end
})

MusicTab:AddButton({
    Name = "Tocar Música 🎵",
    Callback = function()
        if musicId ~= "" then
            local sound = Instance.new("Sound", game.Workspace)
            sound.SoundId = "rbxassetid://" .. musicId
            sound.Volume = 10
            sound.Looped = true
            sound:Play()
        end
    end
})

-- 📌 **SEÇÃO DE HACKS**
HacksTab:AddButton({
    Name = "Super Velocidade ⚡",
    Callback = function()
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100
    end
})

HacksTab:AddButton({
    Name = "Super Pulo 🦘",
    Callback = function()
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = 200
    end
})

HacksTab:AddButton({
    Name = "Atravessar Paredes 🚪",
    Callback = function()
        local char = game.Players.LocalPlayer.Character
        for _, part in pairs(char:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
            end
        end
    end
})

-- 📌 **SEÇÃO DE SCRIPTS**
ScriptsTab:AddButton({
    Name = "Ativar Fly ✈️",
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

-- 📌 **SEÇÃO SOBRE**
AboutTab:AddParagraph("Criado por:", "Shelby, Discord: snobodj")
AboutTab:AddParagraph("Descrição:", "Criado para trollar no Brookhaven RP 😆")

-- Iniciar interface
OrionLib:Init()
