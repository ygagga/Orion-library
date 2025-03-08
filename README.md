-- Carregar a Orion Library
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

-- Criar a janela principal
local Window = OrionLib:MakeWindow({
    Name = "Brookhaven Troll Hub 🤡",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TrollHubConfig"
})

-- Criar as abas
local TrollTab = Window:MakeTab({ Name = "🤡 Troll", Icon = "rbxassetid://4483345998" })
local HacksTab = Window:MakeTab({ Name = "⚡ Hacks", Icon = "rbxassetid://4483345998" })
local ScriptsTab = Window:MakeTab({ Name = "🛠️ Scripts", Icon = "rbxassetid://4483345998" })

-- Variáveis
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local selectedPlayer = nil
local playerList = {}

-- Função para atualizar a lista de jogadores
local function UpdatePlayerList()
    playerList = {}
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            table.insert(playerList, player.Name)
        end
    end
    OrionLib:MakeNotification({
        Name = "Lista Atualizada!",
        Content = "A lista de jogadores foi atualizada.",
        Image = "rbxassetid://4483345998",
        Time = 3
    })
end

-- Atualizar a lista de jogadores ao iniciar
UpdatePlayerList()

-- Dropdown para selecionar um jogador
local Dropdown = TrollTab:AddDropdown({
    Name = "Selecionar Jogador",
    Default = "",
    Options = playerList,
    Callback = function(Value)
        selectedPlayer = Players:FindFirstChild(Value)
    end
})

-- Botão para atualizar a lista de jogadores
TrollTab:AddButton({
    Name = "🔄 Atualizar Lista de Jogadores",
    Callback = function()
        UpdatePlayerList()
        Dropdown:Refresh(playerList, true)
    end
})

-- ESP Toggle
TrollTab:AddToggle({
    Name = "Ativar ESP",
    Default = false,
    Callback = function(State)
        for _, player in pairs(Players:GetPlayers()) do
            if player.Character then
                if State then
                    if not player.Character:FindFirstChild("ESP") then
                        local highlight = Instance.new("Highlight")
                        highlight.Name = "ESP"
                        highlight.Adornee = player.Character
                        highlight.Parent = player.Character
                    end
                else
                    if player.Character:FindFirstChild("ESP") then
                        player.Character:FindFirstChild("ESP"):Destroy()
                    end
                end
            end
        end
    end
})

-- Teleportar para o jogador selecionado
TrollTab:AddButton({
    Name = "Teleportar para o Jogador",
    Callback = function()
        if selectedPlayer and selectedPlayer.Character and LocalPlayer.Character then
            LocalPlayer.Character.HumanoidRootPart.CFrame = selectedPlayer.Character.HumanoidRootPart.CFrame
        end
    end
})

-- Espectar jogador
TrollTab:AddButton({
    Name = "Espectar Jogador",
    Callback = function()
        if selectedPlayer and selectedPlayer.Character then
            LocalPlayer.CameraSubject = selectedPlayer.Character:FindFirstChildWhichIsA("Humanoid")
        end
    end
})

-- Despectar jogador
TrollTab:AddButton({
    Name = "Despectar",
    Callback = function()
        LocalPlayer.CameraSubject = LocalPlayer.Character:FindFirstChildWhichIsA("Humanoid")
    end
})

-- Teleportar todos para você
TrollTab:AddButton({
    Name = "Teleportar Todos para Você",
    Callback = function()
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character then
                player.Character.HumanoidRootPart.CFrame = LocalPlayer.Character.HumanoidRootPart.CFrame
            end
        end
    end
})

-- ⚡ Hacks
HacksTab:AddButton({
    Name = "Ativar Super Velocidade ⚡",
    Callback = function()
        LocalPlayer.Character.Humanoid.WalkSpeed = 100
    end
})

HacksTab:AddButton({
    Name = "Desativar Velocidade ❌",
    Callback = function()
        LocalPlayer.Character.Humanoid.WalkSpeed = 16
    end
})

HacksTab:AddButton({
    Name = "Ativar Pulo Infinito 🦘",
    Callback = function()
        game:GetService("UserInputService").JumpRequest:Connect(function()
            LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
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
        for _, part in pairs(LocalPlayer.Character:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
            end
        end
    end
})

HacksTab:AddButton({
    Name = "Desativar Atravessar Paredes ❌",
    Callback = function()
        for _, part in pairs(LocalPlayer.Character:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = true
            end

       
