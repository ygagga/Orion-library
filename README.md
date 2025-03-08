local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

-- Criando a janela principal da interface
local Window = OrionLib:MakeWindow({
    Name = "Troll Hub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TrollHubConfig"
})

-----------------------------------------------------------
-- Criando as Abas
-----------------------------------------------------------

-- 🕹️ Troll
local TrollTab = Window:MakeTab({
    Name = "Trolls",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- 🎮 Jogadores
local PlayersTab = Window:MakeTab({
    Name = "Jogadores",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- ⚡ Hacks
local HacksTab = Window:MakeTab({
    Name = "Hacks",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- 🧑‍💻 Scripts
local ScriptsTab = Window:MakeTab({
    Name = "Scripts",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-----------------------------------------------------------
-- Funções de Seleção de Jogador e Teleporte
-----------------------------------------------------------

local selectedPlayer = ""

PlayersTab:AddSection("Controle de Jogadores")

-- Input para seleção de jogador
PlayersTab:AddInput("PlayerName", {
    Title = "Nome do Jogador",
    Default = "",
    Placeholder = "Digite o nome do jogador",
    Callback = function(value)
        selectedPlayer = value
    end
})

-- Função para espectar jogador
local isSpectating = false
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

-- Função para despectar (voltar para o jogador original)
local function despectatePlayer()
    local players = game:GetService("Players")
    local localPlayer = players.LocalPlayer
    local camera = game.Workspace.CurrentCamera
    camera.CameraSubject = localPlayer.Character:FindFirstChildOfClass("Humanoid")
    isSpectating = false
end

-- Função para teleportar todos os jogadores para o jogador atual
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

-- Funções de teleportar e espectar no painel
PlayersTab:AddButton({
    Title = "Espectar Jogador 👀",
    Description = "Veja o que o jogador está fazendo",
    Callback = function()
        if selectedPlayer ~= "" then
            spectatePlayer(selectedPlayer)
        end
    end
})

PlayersTab:AddButton({
    Title = "Despectar 🚶‍♂️",
    Description = "Volte para o seu personagem!",
    Callback = function()
        if isSpectating then
            despectatePlayer()
        end
    end
})

PlayersTab:AddButton({
    Title = "Teleportar Todos 🏃‍♂️",
    Description = "Teleporta todos os jogadores para você!",
    Callback = function()
        teleportAllPlayers()
    end
})

-----------------------------------------------------------
-- Funções de ESP
-----------------------------------------------------------

local ESPEnabled = false

local function toggleESP()
    ESPEnabled = not ESPEnabled
    for _, player in pairs(game:GetService("Players"):GetPlayers()) do
        if player.Character then
            local character = player.Character
            if ESPEnabled then
                -- Ativar ESP (exemplo simples)
                local esp = Instance.new("BillboardGui")
                esp.Adornee = character.Head
                esp.Size = UDim2.new(0, 100, 0, 100)
                esp.StudsOffset = Vector3.new(0, 2, 0)
                esp.Parent = character.Head
                esp.Enabled = ESPEnabled
            else
                -- Desativar ESP
                if character.Head:FindFirstChildOfClass("BillboardGui") then
                    character.Head:FindFirstChildOfClass("BillboardGui"):Destroy()
                end
            end
        end
    end
end

-- Toggle para ativar/desativar ESP
TrollTab:AddToggle({
    Title = "Ativar/Desativar ESP",
    Default = false,
    Callback = function(value)
        toggleESP()
    end
})

-----------------------------------------------------------
-- Scripts Universais
-----------------------------------------------------------

ScriptsTab:AddSection("Carregar Scripts")

ScriptsTab:AddButton({
    Title = "RAEL Hub 🔧",
    Description = "Carrega o RAEL Hub.",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Laelmano24/Rael-Hub/main/main.txt"))()
    end
})

ScriptsTab:AddButton({
    Title = "Fly Gui V3 ✈️",
    Description = "Ativa o Fly Gui V3.",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()
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
-- Finalizando a interface
-----------------------------------------------------------

OrionLib:Init()
