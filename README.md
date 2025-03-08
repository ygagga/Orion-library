local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()
local Window = OrionLib:MakeWindow({
    Name = "Troll Hub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TrollHubConfig"
})

-- Abas
local TrollTab = Window:MakeTab({
    Name = "Trolls",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local PlayerTab = Window:MakeTab({
    Name = "Jogadores",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local HacksTab = Window:MakeTab({
    Name = "Hacks",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local ScriptsTab = Window:MakeTab({
    Name = "Scripts",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-----------------------------------------------------------
-- Funções Auxiliares
-----------------------------------------------------------
local selectedPlayer = ""

local function teleportAllPlayers()
    local localPlayer = game.Players.LocalPlayer
    local localHRP = localPlayer.Character:FindFirstChild("HumanoidRootPart")
    if localHRP then
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character and player ~= localPlayer then
                local targetHRP = player.Character:FindFirstChild("HumanoidRootPart")
                if targetHRP then targetHRP.CFrame = localHRP.CFrame end
            end
        end
    end
end

local function spectatePlayer(targetUsername)
    local targetPlayer = game.Players:FindFirstChild(targetUsername)
    if targetPlayer and targetPlayer.Character then
        game.Workspace.CurrentCamera.CameraSubject = targetPlayer.Character:FindFirstChildOfClass("Humanoid")
    end
end

local function despectatePlayer()
    local localPlayer = game.Players.LocalPlayer
    game.Workspace.CurrentCamera.CameraSubject = localPlayer.Character:FindFirstChildOfClass("Humanoid")
end

local function toggleESP()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player.Character then
            local character = player.Character
            if character:FindFirstChild("Head") then
                local esp = character.Head:FindFirstChild("BillboardGui")
                if esp then esp:Destroy() else
                    local newESP = Instance.new("BillboardGui")
                    newESP.Adornee = character.Head
                    newESP.Size = UDim2.new(0, 100, 0, 100)
                    newESP.StudsOffset = Vector3.new(0, 2, 0)
                    newESP.Parent = character.Head
                end
            end
        end
    end
end

-----------------------------------------------------------
-- Abas e Funcionalidades do Painel
-----------------------------------------------------------

-- Jogadores
PlayerTab:AddSection({
    Name = "Controle de Jogadores"
})

PlayerTab:AddDropdown({
    Name = "Selecione o Jogador",
    Default = "Nenhum",
    Options = function()
        local players = {}
        for _, player in pairs(game.Players:GetPlayers()) do
            table.insert(players, player.Name)
        end
        return players
    end,
    Callback = function(value) selectedPlayer = value end
})

PlayerTab:AddButton({
    Name = "Espectar Jogador",
    Callback = function() 
        if selectedPlayer ~= "" then 
            spectatePlayer(selectedPlayer) 
        end 
    end
})

PlayerTab:AddButton({
    Name = "Despectar",
    Callback = despectatePlayer
})

PlayerTab:AddButton({
    Name = "Teleportar Todos",
    Callback = teleportAllPlayers
})

-- Troll
TrollTab:AddToggle({
    Name = "Ativar/Desativar ESP",
    Default = false,
    Callback = toggleESP
})

-- Scripts Universais
ScriptsTab:AddButton({
    Name = "RAEL Hub",
    Callback = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Laelmano24/Rael-Hub/main/main.txt"))() end
})

ScriptsTab:AddButton({
    Name = "Fly Gui V3",
    Callback = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))() end
})

ScriptsTab:AddButton({
    Name = "Sander X",
    Callback = function() loadstring(game:HttpGet('https://raw.githubusercontent.com/sXPiterXs1111/Sanderxv3.30/main/sanderx3.30'))() end
})

OrionLib:Init()
