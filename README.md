-- Carrega a Orion Library
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Orion/main/source"))()

-- Cria a janela principal
local Window = OrionLib:MakeWindow({
    Name = "Brookhaven Troll Hub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "OrionTest"
})

-- Cria as abas
local MainTab = Window:MakeTab({Name = "Principal", Icon = "rbxassetid://4483345998", PremiumOnly = false})
local PlayerTab = Window:MakeTab({Name = "Jogadores", Icon = "rbxassetid://4483345998", PremiumOnly = false})
local ScriptsTab = Window:MakeTab({Name = "Scripts", Icon = "rbxassetid://4483345998", PremiumOnly = false})

-- Função para ativar/desativar ESP
local espEnabled = false
local function toggleESP(state)
    espEnabled = state
    if espEnabled then
        print("ESP ativado")
        -- Código para ativar ESP aqui
    else
        print("ESP desativado")
        -- Código para desativar ESP aqui
    end
end

-- Toggle para ESP
MainTab:AddToggle({
    Name = "Ativar ESP",
    Default = false,
    Callback = function(value)
        toggleESP(value)
    end
})

-- Atualizar a lista de jogadores
local playerList = {}
local function updatePlayers()
    playerList = {}
    for _, player in pairs(game.Players:GetPlayers()) do
        table.insert(playerList, player.Name)
    end
end

updatePlayers()

-- Dropdown para selecionar jogador
local selectedPlayer
PlayerTab:AddDropdown({
    Name = "Selecionar Jogador",
    Default = "",
    Options = playerList,
    Callback = function(value)
        selectedPlayer = value
        print("Selecionado:", value)
    end
})

-- Botão para atualizar a lista de jogadores
PlayerTab:AddButton({
    Name = "Atualizar Jogadores",
    Callback = function()
        updatePlayers()
        OrionLib:MakeNotification({Name = "Atualizado", Content = "Lista de jogadores atualizada!", Time = 2})
    end
})

-- Função para teleportar para o jogador
local function teleportToPlayer()
    if selectedPlayer then
        local target = game.Players:FindFirstChild(selectedPlayer)
        if target and target.Character and game.Players.LocalPlayer.Character then
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = target.Character.HumanoidRootPart.CFrame
            print("Teleportado para", selectedPlayer)
        end
    end
end

-- Botão para teleportar para o jogador selecionado
PlayerTab:AddButton({
    Name = "Teleportar para o jogador",
    Callback = function()
        teleportToPlayer()
    end
})

-- Função para spectar jogador
local function spectatePlayer()
    if selectedPlayer then
        local target = game.Players:FindFirstChild(selectedPlayer)
        if target and target.Character then
            game.Workspace.Camera.CameraSubject = target.Character.Humanoid
            print("Spectando", selectedPlayer)
        end
    end
end

-- Botão para spectar jogador selecionado
PlayerTab:AddButton({
    Name = "Spectar Jogador",
    Callback = function()
        spectatePlayer()
    end
})

-- Botão para parar de spectar
PlayerTab:AddButton({
    Name = "Parar de Spectar",
    Callback = function()
        game.Workspace.Camera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
        print("Parou de spectar")
    end
})

-- Função para teleportar todos os jogadores para você
local function teleportAllPlayers()
    local localPlayer = game.Players.LocalPlayer
    if localPlayer.Character then
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= localPlayer and player.Character then
                player.Character.HumanoidRootPart.CFrame = localPlayer.Character.HumanoidRootPart.CFrame
            end
        end
        print("Todos os jogadores foram teleportados para você")
    end
end

-- Botão para teleportar todos os jogadores para você
PlayerTab:AddButton({
    Name = "Teleportar Todos para Mim",
    Callback = function()
        teleportAllPlayers()
    end
})

-- Botão para executar RAEL Hub
ScriptsTab:AddButton({
    Name = "Executar RAEL Hub",
    Callback = function()
        loadstring(game:HttpGet("URL_DO_RAEL_HUB_AQUI"))()
    end
})

-- Botão para executar Fly GUI v3
ScriptsTab:AddButton({
    Name = "Executar Fly GUI v3",
    Callback = function()
        loadstring(game:HttpGet("URL_DO_FLY_GUI_AQUI"))()
    end
})

-- Botão para executar SANDER X
ScriptsTab:AddButton({
    Name = "Executar SANDER X",
    Callback = function()
        loadstring(game:HttpGet("URL_DO_SANDER_X_AQUI"))()
    end
})

-- Inicia a UI
OrionLib:Init()
