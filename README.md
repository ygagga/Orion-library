-- Iniciar a biblioteca Orion
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

-- Criando a janela principal da interface
local Window = OrionLib:MakeWindow({
    Name = "Troll Hub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TrollHubConfig"
})

-- Funções auxiliares

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

-- Controle de jogadores
local selectedPlayer = ""
local isSpectating = false

-- Função para teleportar todos os jogadores
local function teleportAllPlayers()
    local players = game:GetService("Players")
    local localPlayer = players.LocalPlayer
    local localHumanoidRootPart = localPlayer.Character:FindFirstChild("HumanoidRootPart")

    if localHumanoidRootPart then
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

-- Função para despectar
local function despectatePlayer()
    local players = game:GetService("Players")
    local localPlayer = players.LocalPlayer
    local camera = game.Workspace.CurrentCamera
    camera.CameraSubject = localPlayer.Character:FindFirstChildOfClass("Humanoid")
    isSpectating = false
end

-- Hacks
local speedActive = false
local jumpActive = false
local wallWalkActive = false

-- Função para ativar/desativar super velocidade
local function toggleSpeed(active)
    if active then
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100
    else
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
    end
    speedActive = active
end

-- Função para ativar/desativar pulo infinito
local function toggleJump(active)
    if active then
        game:GetService("UserInputService").JumpRequest:Connect(function()
            game.Players.LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        end)
    else
        game:GetService("UserInputService").JumpRequest:Disconnect()
    end
    jumpActive = active
end

-- Função para ativar/desativar atravessar paredes
local function toggleWallWalk(active)
    local player = game.Players.LocalPlayer
    local character = player.Character
    local function enableWallWalk()
        for _, part in pairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = not active
            end
        end
    end
    enableWallWalk()
    wallWalkActive = active
end

-- Função para tocar música para todos os jogadores
local musicId = ""
local loopMusic = false
local musicPlaying = nil

local function playMusicForAll(id, loop)
    if musicPlaying then
        musicPlaying:Stop()
        musicPlaying:Destroy()
    end

    musicPlaying = Instance.new("Sound")
    musicPlaying.SoundId = "rbxassetid://" .. id
    musicPlaying.Looped = loop
    musicPlaying.Volume = 1
    musicPlaying.Parent = game:GetService("Workspace")
    musicPlaying:Play()
end

-----------------------------------------------------------
-- Criando as Abas
-----------------------------------------------------------

-- Trolls
local TrollTab = Window:MakeTab({
    Name = "Trolls",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

TrollTab:AddSection("Controle de Jogadores")

TrollTab:AddInput("PlayerName", {
    Title = "Nome do Jogador",
    Default = "",
    Placeholder = "Digite o nome do jogador",
    Callback = function(value)
        selectedPlayer = value
    end
})

TrollTab:AddButton({
    Title = "Teleportar Todos 🏃‍♂️",
    Description = "Teleporta todos os jogadores para você!",
    Callback = function()
        teleportAllPlayers()
    end
})

TrollTab:AddButton({
    Title = "Espectar 👀",
    Description = "Veja o que o jogador está fazendo",
    Callback = function()
        if selectedPlayer ~= "" then
            spectatePlayer(selectedPlayer)
        end
    end
})

TrollTab:AddButton({
    Title = "Despectar 🚶‍♂️",
    Description = "Volte para o seu personagem!",
    Callback = function()
        if isSpectating then
            despectatePlayer()
        end
    end
})

-----------------------------------------------------------
-- Música
-----------------------------------------------------------

local MusicTab = Window:MakeTab({
    Name = "Música",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

MusicTab:AddSection("Reproduzir Música para Todos")

MusicTab:AddInput("MusicID", {
    Title = "ID da Música",
    Default = "",
    Placeholder = "Digite o ID da música",
    Numeric = true,
    Finished = true,
    Callback = function(value)
        musicId = value
    end
})

MusicTab:AddToggle("LoopMusic", {
    Title = "Loop",
    Default = false,
    Callback = function(value)
        loopMusic = value
    end
})

MusicTab:AddButton({
    Title = "Reproduzir Música 🎶",
    Description = "Reproduza a música para todos os jogadores.",
    Callback = function()
        if musicId ~= "" then
            playMusicForAll(musicId, loopMusic)
        end
    end
})

-----------------------------------------------------------
-- Hacks
-----------------------------------------------------------

local HacksTab = Window:MakeTab({
    Name = "Hacks",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

HacksTab:AddSection("Superpoderes!")

HacksTab:AddButton({
    Title = "Ativar Super Velocidade ⚡",
    Description = "Corre mais rápido que o Flash!",
    Callback = function()
        toggleSpeed(true)
    end
})

HacksTab:AddButton({
    Title = "Desativar Velocidade ❌",
    Description = "Desativa a Super Velocidade!",
    Callback = function()
        toggleSpeed(false)
    end
})

HacksTab:AddButton({
    Title = "Ativar Pulo Infinito 🦘",
    Description = "Pule o quanto quiser sem limites!",
    Callback = function()
        toggleJump(true)
    end
})

HacksTab:AddButton({
    Title = "Desativar Pulo Infinito ❌",
    Description = "Desativa o Pulo Infinito!",
    Callback = function()
        toggleJump(false)
    end
})

HacksTab:AddButton({
    Title = "Ativar Atravessar Paredes 🚪",
    Description = "Agora você pode atravessar as paredes!",
    Callback = function()
        toggleWallWalk(true)
    end
})

HacksTab:AddButton({
    Title = "Desativar Atravessar Paredes ❌",
    Description = "Desativa o poder de atravessar paredes!",
    Callback = function()
        toggleWallWalk(false)
    end
})

-----------------------------------------------------------
-- Scripts
-----------------------------------------------------------

local ScriptsTab = Window:MakeTab({
    Name = "Scripts",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

ScriptsTab:AddSection("Carregar Scripts")

ScriptsTab:AddButton({
    Title = "Fly Script ✈️",
    Description = "Ativa o Fly script.",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()
    end
})

ScriptsTab:AddButton({
    Title = "RAEL Hub 🔧",
    Description = "Carrega o RAEL Hub.",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Laelmano24/Rael-Hub/main/main.txt"))()
    end
})

ScriptsTab:AddButton({
    Title = "Sander X 🛸",
    Description = "Carrega o Sander X.",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/sXPiterXs1111/Sanderxv3.30/main/sanderx3.30'))()
    end
})

-----------------------------------------------------------
-- Sobre
-----------------------------------------------------------

local AboutTab = Window:MakeTab({
    Name = "Sobre",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

AboutTab:AddSection("Informações do Criador")

AboutTab:AddParagraph("Criado por Shelby, Discord: snobodj")
AboutTab:AddParagraph("Criado para bagunçar no Brookhaven RP! Aproveite e divirta-se, mas sem exagerar! 😆")

    
