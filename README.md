-- Carregar a Orion Library
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

-- Criar a Janela Principal
local Window = OrionLib:MakeWindow({
    Name = "Troll Hub",
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
        -- Código para lagar o servidor
        print("Lag ativado")
    end
})

-- Botão para Aumentar a Velocidade do Jogador
TrollTab:AddButton({
    Name = "Super Velocidade",
    Callback = function()
        local player = game.Players.LocalPlayer
        if player.Character then
            player.Character.Humanoid.WalkSpeed = 100 -- Ajuste a velocidade conforme necessário
        end
        print("Velocidade aumentada")
    end
})

-- Botão para Spawnar um Sofá Matador
TrollTab:AddButton({
    Name = "Spawnar Sofá Matador",
    Callback = function()
        -- Código para spawnar sofá e matar o alvo
        print("Sofá matador ativado")
    end
})

-- Botão para Teleportar um Jogador para sua Casa
TrollTab:AddButton({
    Name = "Trazer Jogador para sua Casa",
    Callback = function()
        -- Código para teleportar um jogador
        print("Jogador teleportado")
    end
})

-- Botão para Copiar Skin de Outro Jogador
TrollTab:AddButton({
    Name = "Copiar Skin de Alguém",
    Callback = function()
        -- Código para copiar a skin
        print("Skin copiada")
    end
})

-- Criar Dropdown para Selecionar um Jogador
local SelectedPlayer = nil
local playersList = {}

for _, player in pairs(game.Players:GetPlayers()) do
    table.insert(playersList, player.Name)
end

TrollTab:AddDropdown({
    Name = "Selecionar Jogador",
    Default = playersList[1] or "Nenhum",
    Options = playersList,
    Callback = function(value)
        SelectedPlayer = value
        print("Jogador selecionado:", value)
    end
})

-- Botão para Teleportar Jogador Selecionado
TrollTab:AddButton({
    Name = "Teleportar Jogador Selecionado",
    Callback = function()
        if SelectedPlayer then
            -- Código para teleportar o jogador selecionado
            print("Teleportando:", SelectedPlayer)
        end
    end
})

-- Botão para Matar o Jogador Selecionado
TrollTab:AddButton({
    Name = "Matar Jogador Selecionado",
    Callback = function()
        if SelectedPlayer then
            -- Código para matar o jogador selecionado
            print("Matando:", SelectedPlayer)
        end
    end
})

-- Finalizar a Interface (OBRIGATÓRIO)
OrionLib:Init()
