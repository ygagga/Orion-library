-- Iniciar a biblioteca Orion
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

-- Criando a janela principal da interface
local Window = OrionLib:MakeWindow({
    Name = "Troll Hub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TrollHubConfig"
})

-- Criando as abas
local TrollTab = Window:MakeTab({
    Name = "Trolls",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-----------------------------------------------------------
-- Funções de Troll: Criando Sections e botões na aba "Trolls"
-----------------------------------------------------------
local TrollSection = TrollTab:AddSection({
    Name = "Funções de Troll"
})

-- Função para Matar Jogador
TrollSection:AddButton({
    Name = "Matar Jogador",
    Callback = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/ygagga/Tetsw/refs/heads/main/README.md"))()
        print("Jogador Morto!")
        -- Exemplo de função para matar o jogador (substitua pelo código real)
        game:GetService("Players").LocalPlayer.Character:BreakJoints()
    end
})

-- Função para Teleportar Jogador
TrollSection:AddButton({
    Name = "Teleportar Jogador",
    Callback = function()
        -- Aqui você pode colocar o código para teleportar um jogador
        local targetPlayer = game:GetService("Players"):GetPlayerByName("PlayerName") -- Substitua pelo nome do jogador
        local targetCharacter = targetPlayer.Character
        targetCharacter:MoveTo(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position) -- Teleportando o alvo para o jogador
        print("Jogador Teleportado!")
    end
})

-- Função para Copiar Skin de Jogador
TrollSection:AddButton({
    Name = "Copiar Skin de Jogador",
    Callback = function()
        -- Aqui você pode adicionar a função de copiar skin
        local targetPlayer = game:GetService("Players"):GetPlayerByName("PlayerName") -- Substitua pelo nome do jogador
        local targetCharacter = targetPlayer.Character
        -- Clone a skin
        game:GetService("Players").LocalPlayer.Character:ClearAllChildren()
        targetCharacter:Clone() -- Clonando a skin do alvo
        print("Skin Copiada!")
    end
})

-----------------------------------------------------------
-- Funções de Admin: Criando Sections e botões na aba "Admin"
-----------------------------------------------------------
local AdminTab = Window:MakeTab({
    Name = "Admin",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local AdminSection = AdminTab:AddSection({
    Name = "Funções de Admin"
})

-- Função para Banir Jogador
AdminSection:AddButton({
    Name = "Banir Jogador",
    Callback = function()
        -- Código para banir jogador
        print("Jogador Banido!")
        local targetPlayer = game:GetService("Players"):GetPlayerByName("PlayerName") -- Substitua pelo nome do jogador
        targetPlayer:Kick("Banido!")
    end
})

-- Função para Ban Automático
AdminSection:AddButton({
    Name = "Aplicar Ban Automático",
    Callback = function()
        -- Código para banir automaticamente
        print("Ban Automático Aplicado!")
        local targetPlayer = game:GetService("Players"):GetPlayerByName("PlayerName") -- Substitua pelo nome do jogador
        targetPlayer:Kick("Banido automaticamente!")
    end
})

-- Finalizando a interface
OrionLib:Init()
