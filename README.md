-- Carrega a biblioteca Orion
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/yaoclub/Orion/master/OrionLib.lua"))()

-- Criando a Janela da Interface
local Window = OrionLib:MakeWindow({
    Name = "Brookhaven RP 🏡 (Troll Hub 🤡)",
    HidePremium = false,
    IntroEnabled = true,
    SaveConfig = true
})

-- Função para trocar a cabeça do avatar
local function changeAvatar(id, notificationTitle)
    local argsTable = (type(id) == "table") and id or {1, 1, 1, 1, 1, id}

    local args = {
        [1] = "CharacterChange",
        [2] = argsTable,
        [3] = "🔥 Troll Hub 💀"
    }

    local replicatedStorage = game:GetService("ReplicatedStorage")
    local starterGui = game:GetService("StarterGui")

    if replicatedStorage and starterGui then
        local remote = replicatedStorage.RE:FindFirstChild("1Avata1rOrigina1l")
        if remote then
            remote:FireServer(unpack(args))
            starterGui:SetCore("SendNotification", {
                Title = notificationTitle,
                Text = "Aguarde 1-10 segundos...",
                Duration = 5
            })
        end
    end
end

-----------------------------------------------------------
-- 🤡 Troll (ESP)
-----------------------------------------------------------
local TrollTab = Window:MakeTab({
    Name = "🤡 Troll",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Adiciona uma seção para controle de jogadores na aba Troll
TrollTab:AddSection({
    Name = "Controle de Jogadores"
})

local selectedPlayer = ""
local isSpectating = false  -- Variável para controlar o espectar

-- Campo de entrada para o nome do jogador
TrollTab:AddTextbox({
    Name = "Nome do Jogador",
    Default = "",
    TextDisappear = true,
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

-- Função para despectar (retornar a câmera para o jogador original)
local function despectatePlayer()
    local players = game:GetService("Players")
    local localPlayer = players.LocalPlayer
    local camera = game.Workspace.CurrentCamera
    camera.CameraSubject = localPlayer.Character:FindFirstChildOfClass("Humanoid")
    isSpectating = false
end

-- Botão para teleportar todos os jogadores para o jogador
TrollTab:AddButton({
    Name = "Teleportar Todos 🏃‍♂️",
    Callback = function()
        teleportAllPlayers()
    end
})

-- Botão para espectar o jogador
TrollTab:AddButton({
    Name = "Espectar 👀",
    Callback = function()
        if selectedPlayer ~= "" then
            spectatePlayer(selectedPlayer)
        end
    end
})

-- Botão para despectar (voltar para o jogador original)
TrollTab:AddButton({
    Name = "Despectar 🚶‍♂️",
    Callback = function()
        if isSpectating then
            despectatePlayer()
        end
    end
})

-----------------------------------------------------------
-- 🎶 Música
-----------------------------------------------------------
local MusicTab = Window:MakeTab({
    Name = "🎶 Música",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local musicId = ""  -- ID da música a ser tocada
local loopMusic = false  -- Controle de loop da música
local musicPlaying = nil  -- Armazena o som que está tocando

-- Função para tocar música em loop para todos os jogadores
local function playMusicForAll(id, loop)
    -- Checa se já existe uma música tocando, e se sim, para ela
    if musicPlaying then
        musicPlaying:Stop()
        musicPlaying:Destroy()
    end

    -- Cria um novo objeto de som no Workspace
    musicPlaying = Instance.new("Sound")
    musicPlaying.SoundId = "rbxassetid://" .. id
    musicPlaying.Looped = loop
    musicPlaying.Volume = 1  -- Volume máximo
    musicPlaying.Parent = game:GetService("Workspace")  -- Coloca o som no Workspace, assim todos podem ouvir

    musicPlaying:Play()
end

-- Campo de entrada para o ID da música
MusicTab:AddTextbox({
    Name = "ID da Música",
    Default = "",
    TextDisappear = true,
    Callback = function(value)
        musicId = value
    end
})

-- Campo de seleção para o loop da música
MusicTab:AddToggle({
    Name = "Loop",
    Default = false,
    Callback = function(value)
        loopMusic = value
    end
})

-- Botão para iniciar a música para todos os jogadores
MusicTab:AddButton({
    Name = "Reproduzir Música 🎶",
    Callback = function()
        if musicId ~= "" then
            playMusicForAll(musicId, loopMusic)
        end
    end
})

-----------------------------------------------------------
-- ⚡ Hacks (Velocidade + Pulo Infinito + Atravessar Paredes)
-----------------------------------------------------------
local HacksTab = Window:MakeTab({
    Name = "⚡ Hacks",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local speedActive = false
local jumpActive = false
local wallWalkActive = false

HacksTab:AddSection({
    Name = "Superpoderes!"
})

-- Velocidade infinita
HacksTab:AddButton({
    Name = "Ativar Super Velocidade ⚡",
    Callback = function()
        speedActive = true
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100
    end
})

-- Desativar Velocidade
HacksTab:AddButton({
    Name = "Desativar Velocidade ❌",
    Callback = function()
        speedActive = false
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
    end
})

-- Pulo infinito
HacksTab:AddButton({
    Name = "Ativar Pulo Infinito 🦘",
    Callback = function()
        jumpActive = true
        game:GetService("UserInputService").JumpRequest:Connect(function()
            game.Players.LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        end)
    end
})

-- Desativar Pulo Infinito
HacksTab:AddButton({
    Name = "Desativar Pulo Infinito ❌",
    Callback = function()
        jumpActive = false
        -- Desconectar a função de pulo infinito
        game:GetService("UserInputService").JumpRequest:Disconnect()
    end
})

-- Atravessar Paredes
HacksTab:AddButton({
    Name = "Ativar Atravessar Paredes 🚪",
    Callback = function()
        wallWalkActive = true
        local player = game.Players.LocalPlayer
        local character = player.Character
        local humanoid = character:WaitForChild("Humanoid")

        local function enableWallWalk()
            for _, part in pairs(character:GetChildren()) do
                if part:IsA("BasePart") then
                    part.CanCollide = false
                end
            end
        end

        enableWallWalk()
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "Poder Ativado!",
            Text = "Você agora pode atravessar paredes! 🚪",
            Duration = 5
        })
    end
})

-- Desativar Atravessar Paredes
HacksTab:AddButton({
    Name = "Desativar Atravessar Paredes ❌",
    Callback = function()
        wallWalkActive = false
        local player = game.Players.LocalPlayer
        local character = player.Character

        local function disableWallWalk()
            for _, part in pairs(character:GetChildren()) do
                if part:IsA("BasePart") then
                    part.CanCollide = true
                end
            end
        end

        disableWallWalk()
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
local ScriptsTab = Window:MakeTab({
    Name = "🧑‍💻 Scripts",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Adiciona os scripts na aba Scripts
ScriptsTab:AddSection({
    Name = "Carregar Scripts"
})

-- Botões para carregar os scripts
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
        loadstring(game:HttpGet('https://raw.githubusercontent.com/sXPiterXs1111/Sanderxv3.30/main/sanderx3.30'))()
    end
})

-----------------------------------------------------------
-- Fechar a interface
OrionLib:Init()
