local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

-- Criando a janela
local Window = OrionLib:MakeWindow({
    Name = "Exemplo de Interface",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "ExemploConfig"
})

-- Criando as Tabs
local Tab1 = Window:MakeTab({
    Name = "Trolls",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local Tab2 = Window:MakeTab({
    Name = "Admin",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Adicionando uma Section na Tab1
local Section1 = Tab1:AddSection({
    Name = "Funções de Troll"
})

-- Adicionando um botão na Section1
Section1:AddButton({
    Name = "Matar Jogador",
    Callback = function()
        -- Ação para matar o jogador
        print("Jogador Morto!")
    end
})

-- Adicionando outra Section na Tab2
local Section2 = Tab2:AddSection({
    Name = "Funções de Admin"
})

-- Adicionando um botão na Section2
Section2:AddButton({
    Name = "Teleportar Jogador",
    Callback = function()
        -- Ação para teleportar o jogador
        print("Jogador Teleportado!")
    end
})

-- Finalizando a interface
OrionLib:Init()
