local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

-- Criando a Janela da Interface
local Window = OrionLib:MakeWindow({
    Name = "Brookhaven RP 🏡 (Troll Hub 🤡)",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TrollHubConfig"
})

-- Criando as Abas
local Tabs = {
    Troll = Window:MakeTab({
        Name = "🤡 Troll",
        Icon = "rbxassetid://4483345998",
        PremiumOnly = false
    }),
    Music = Window:MakeTab({
        Name = "🎶 Música",
        Icon = "rbxassetid://4483345998",
        PremiumOnly = false
    }),
    Hacks = Window:MakeTab({
        Name = "⚡ Hacks",
        Icon = "rbxassetid://4483345998",
        PremiumOnly = false
    }),
    Scripts = Window:MakeTab({
        Name = "🧑‍💻 Scripts",
        Icon = "rbxassetid://4483345998",
        PremiumOnly = false
    }),
    About = Window:MakeTab({
        Name = "ℹ️ Sobre",
        Icon = "rbxassetid://4483345998",
        PremiumOnly = false
    })
}

-----------------------------------------------------------
-- 🤡 Troll
-----------------------------------------------------------
TabTroll:AddSection({
    Name = "Controle de Jogadores"
})

local selectedPlayer = ""
local isSpectating = false

TabTroll:AddInput({
    Name = "Nome do Jogador",
    Default = "",
    Placeholder = "Digite o nome do jogador",
    Callback = function(value)
        selectedPlayer = value
    end
})

-- Função para teleportar todos os jogadores para o local do jogador que executou o comando
local function teleportAllPlayers()
    local players = game:GetService("Players")
    local localPlayer = players.LocalPlayer
    local localHumanoidRootPart = localPlayer.Character:FindFirstChild("HumanoidRootPart")

    if localHumanoidRootPart then
        -- Teleportando todos os jogadores para a posição do jogador atual
        for _, targetPlayer in pairs(players:GetPlayers()) do
            if targetPlayer.Character and targetPlayer ~= localPlayer then
                local targetHumanoidRootPart = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
                if targetHumanoidRootPart then
                    targetHumanoidRootPart.CFrame = localHumanoidRootPart.CFrame
                end
            end
        end
    end
end

-- Função para espectar o jogador
local function spectatePlayer(targetUsername)
    local players = game:GetService("Players")
    local localPlayer = players.LocalPlayer
    local targetPlayer = players:FindFirstChild(targetUsername)

    if targetPlayer and targetPlayer.Character then
        local camera = game.Workspace.CurrentCamera
        camera.CameraSubject = targetPlayer.Character:FindFirstChildOfClass("Humanoid")
        isSpectating = true
    end
end

-- Função para despectar (voltar a câmera para o jogador original)
local function despectatePlayer()
    local players = game:GetService("Players")
    local localPlayer = players.LocalPlayer
    local camera = game.Workspace.CurrentCamera
    camera.CameraSubject = localPlayer.Character:FindFirstChildOfClass("Humanoid")
    isSpectating = false
end

TabTroll:AddButton({
    Name = "Teleportar Todos 🏃‍♂️",
    Description = "Teleporta todos os jogadores para você!",
    Callback = function()
        teleportAllPlayers()
    end
})

Tabs.Troll:AddButton({
    Name = "Espectar 👀",
    Description = "Veja o que o jogador está fazendo",
    Callback = function()
        if selectedPlayer ~= "" then
            spectatePlayer(selectedPlayer)
        end
    end
})

TabTroll:AddButton({
    Name = "Despectar 🚶‍♂️",
    Description = "Volte para o seu personagem!",
    Callback = function()
        if isSpectating then
            despectatePlayer()
        end
    end
})

-----------------------------------------------------------
-- 🎶 Música
-----------------------------------------------------------
TabMusic:AddSection({
    Name = "Reproduzir Música para Todos"
})

local musicId = ""  -- ID da música a ser tocada
local loopMusic = false  -- Controle de loop da música

local function playMusicForAll(id, loop)
    -- Checa se já existe uma música tocando, e se sim, para ela
    local musicPlaying = game:GetService("Workspace"):FindFirstChild("MusicPlaying")
    if musicPlaying then
        musicPlaying:Stop()
        musicPlaying:Destroy()
    end

    -- Cria um novo objeto de som no Workspace
    musicPlaying = Instance.new("Sound")
    musicPlaying.Name = "MusicPlaying"
    musicPlaying.SoundId = "rbxassetid://" .. id
    musicPlaying.Looped = loop
    musicPlaying.Volume = 1
    musicPlaying.Parent = game:GetService("Workspace")

    musicPlaying:Play()
end

TabMusic:AddInput({
    Name = "ID da Música",
    Default = "",
    Placeholder = "Digite o ID da música",
    Numeric = true,
    Finished = true,
    Callback = function(value)
        musicId = value
    end
})

TabMusic:AddToggle({
    Name = "Loop",
    Default = false,
    Callback = function(value)
        loopMusic = value
    end
})

TabMusic:AddButton({
    Name = "Reproduzir Música 🎶",
    Description = "Reproduza a música para todos os jogadores.",
    Callback = function()
        if musicId ~= "" then
            playMusicForAll(musicId, loopMusic)
        end
    end
})

-----------------------------------------------------------
-- ⚡ Hacks
-----------------------------------------------------------
TabHacks:AddSection({
    Name = "Superpoderes!"
})

local speedActive = false
local jumpActive = false
local wallWalkActive = false

Tabs.Hacks:AddButton({
    Name = "Ativar Super Velocidade ⚡",
    Description = "Corre mais rápido que o Flash!",
    Callback = function()
        speedActive = true
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100
    end
})

TabHacks:AddButton({
    Name = "Desativar Velocidade ❌",
    Description = "Desativa a Super Velocidade!",
    Callback = function()
        speedActive = false
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
    end
})

TabHacks:AddButton({
    Name = "Ativar Pulo Infinito 🦘",
    Description = "Pule o quanto quiser sem limites!",
    Callback = function()
        jumpActive = true
        game:GetService("UserInputService").JumpRequest:Connect(function()
            game.Players.LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        end)
    end
})

TabHacks:AddButton({
    Name = "Desativar Pulo Infinito ❌",
    Description = "Desativa o Pulo Infinito!",
    Callback = function()
        jumpActive = false
        game:GetService("UserInputService").JumpRequest:Disconnect()
    end
})

TabHacks:AddButton({
    Name = "Ativar Atravessar Paredes 🚪",
    Description = "Agora você pode atravessar as paredes!",
    Callback = function()
        wallWalkActive = true
        local player = game.Players.LocalPlayer
        local character = player.Character
        local humanoid = character:WaitForChild("Humanoid")

        for _, part in pairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
            end
        end
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "Poder Ativado!",
            Text = "Você agora pode atravessar paredes! 🚪",
            Duration = 5
        })
    end
})

TabHacks:AddButton({
    Name = "Desativar Atravessar Paredes ❌",
    Description = "Desativa o poder de atravessar paredes!",
    Callback = function()
        wallWalkActive = false
        local player = game.Players.LocalPlayer
        local character = player.Character

        for _, part in pairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = true
            end
        end
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "Poder Desativado",
            Text = "Você não pode mais atravessar paredes.",
            Duration = 5
        })
    end
})

-----------------------------------------------------------
-- 🧑‍💻 Scripts
-----------------------------------------------------------
TabScripts:AddSection({
    Name = "Carregar Scripts"
})

TabScripts:AddButton({
    Name = "Fly Script ✈️",
    Description = "Ativa o Fly script.",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()
    end
})

TabScripts:AddButton({
    Name = "RAEL Hub 🔧",
    Description = "Carrega o RAEL Hub.",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Laelmano24/Rael-Hub/main/main.txt"))()
    end
})

TabScripts:AddButton({
    Name = "Sander X 🛸",
    Description = "Carrega o Sander X.",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/sXPiterXs1111/Sanderxv3.30/main/sanderx3.30'))()
    end
})

-----------------------------------------------------------
-- ℹ️ Sobre
-----------------------------------------------------------
TabAbout:AddSection({
    Name = "Criado por Shelby"
})

TabAbout:AddParagraph("Criado por Troll Hub para bagunçar no Brookhaven RP!")
TabAbout:AddParagraph("Aproveite e divirta-se, mas sem exagerar! 😆")

-- Finalizando a Interface
OrionLib:Init()
