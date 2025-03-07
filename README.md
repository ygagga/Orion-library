-- Carregar a Orion Library
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/jensonhirst/Orion/main/source"))()

-- Criar a Janela Principal
local Window = OrionLib:MakeWindow({
    Name = "Troll Hub 🤡",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TrollHubConfig"
})

-- Criar uma Aba Principal
local TrollTab = Window:MakeTab({
    Name = "Troll Options",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Seção do Menu de Troll
local TrollSection = TrollTab:AddSection({
    Name = "Funções de Troll"
})

-- Botão para Lagar o Servidor
TrollTab:AddButton({
    Name = "Lagar o Servidor",
    Callback = function()
        while true do
            game:GetService("RunService").Heartbeat:Wait()
        end
    end
})

-- Botão para Aumentar a Velocidade do Jogador
TrollTab:AddButton({
    Name = "Super Velocidade ⚡",
    Callback = function()
        local player = game.Players.LocalPlayer
        if player.Character then
            player.Character.Humanoid.WalkSpeed = 100
        end
    end
})

-- Botão para Spawnar um Sofá Matador
TrollTab:AddButton({
    Name = "Spawnar Sofá Matador ☠️",
    Callback = function()
        local player = game.Players.LocalPlayer
        local char = player.Character
        if char then
            local sofa = Instance.new("Part", workspace)
            sofa.Size = Vector3.new(5, 1, 3)
            sofa.Position = char.HumanoidRootPart.Position
            sofa.Touched:Connect(function(hit)
                if hit.Parent:FindFirstChild("Humanoid") then
                    hit.Parent.Humanoid.Health = 0
                end
            end)
        end
    end
})

-- Botão para Teleportar um Jogador para sua Casa
TrollTab:AddButton({
    Name = "Trazer Jogador para sua Casa 🏠",
    Callback = function()
        local player = game.Players.LocalPlayer
        local char = player.Character
        if char then
            for _, p in pairs(game.Players:GetPlayers()) do
                if p ~= player and p.Character then
                    p.Character.HumanoidRootPart.CFrame = char.HumanoidRootPart.CFrame
                end
            end
        end
    end
})

-- Botão para Copiar Skin de Outro Jogador
TrollTab:AddButton({
    Name = "Copiar Skin de Alguém 🎭",
    Callback = function()
        local player = game.Players.LocalPlayer
        if SelectedPlayer then
            local target = game.Players:FindFirstChild(SelectedPlayer)
            if target and target.Character then
                local char = player.Character
                for _, item in pairs(target.Character:GetChildren()) do
                    if item:IsA("Accessory") or item:IsA("Clothing") then
                        item:Clone().Parent = char
                    end
                end
            end
        end
    end
})

-- Criar Dropdown para Selecionar um Jogador
local SelectedPlayer = nil
TrollTab:AddDropdown({
    Name = "Selecionar Jogador 🎯",
    Default = "Nenhum",
    Options = {},
    Callback = function(value)
        SelectedPlayer = value
    end
})

-- Atualizar a Lista de Jogadores
local function UpdatePlayers()
    local playersList = {}
    for _, player in pairs(game.Players:GetPlayers()) do
        table.insert(playersList, player.Name)
    end
    TrollTab:RefreshDropdown({
        Name = "Selecionar Jogador 🎯",
        Options = playersList,
    })
end

-- Atualiza a lista automaticamente quando um jogador entra ou sai
game.Players.PlayerAdded:Connect(UpdatePlayers)
game.Players.PlayerRemoving:Connect(UpdatePlayers)
UpdatePlayers()

-- Botão para Teleportar Jogador Selecionado
TrollTab:AddButton({
    Name = "Teleportar Jogador Selecionado ✨",
    Callback = function()
        if SelectedPlayer then
            local localPlayer = game.Players.LocalPlayer
            local target = game.Players:FindFirstChild(SelectedPlayer)
            if target and target.Character and localPlayer.Character then
                local myHRP = localPlayer.Character:FindFirstChild("HumanoidRootPart")
                local targetHRP = target.Character:FindFirstChild("HumanoidRootPart")
                if myHRP and targetHRP then
                    targetHRP.CFrame = myHRP.CFrame
                end
            end
        end
    end
})

-- Botão para Matar o Jogador Selecionado
TrollTab:AddButton({
    Name = "Matar Jogador Selecionado 💀",
    Callback = function()
        if SelectedPlayer then
            local target = game.Players:FindFirstChild(SelectedPlayer)
            if target and target.Character and target.Character:FindFirstChild("Humanoid") then
                target.Character.Humanoid.Health = 0
            end
        end
    end
})

-- Finalizar a Interface
OrionLib:Init()
