-- Iniciar a biblioteca Orion
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

-- Criando a janela principal da interface
local Window = OrionLib:MakeWindow({
    Name = "👾Zenith core Hub👾",
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

local SciptTab = Window:MakeTab({
    Name = "🪐Scipts universais",
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

-- Função para Teleportar players
TrollSection:AddButton({
    Name = "Teleportar Todos os players",
    Callback = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/ygagga/SCIPTER-TUBERS93/refs/heads/main/README.md"))()
       print("Jogadores Teleportados!")
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
local SciptTab = Window:MakeTab({
    Name = "🪐Scipts universais",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local SciptSection = AdminTab:AddSection({
    Name = "Scipts Universais Abaixo"
})

-- Função para Banir Jogador
SciptSection:AddButton({
    Name = "Rael hub",
    Callback = function()
      loadstring(game:HttpGet("https://raw.githubusercontent.com/Laelmano24/Rael-Hub/main/main.txt"))() 
        print("Scipt Carregado Com Sucesso!")       
    end
})

-- Função para Ban Automático
AdminSection:AddButton({
    Name = "Fly Gui🛩️",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/mikeexc/Dsc-Mike-Fly-Gui/main/Fly%20Gui"))()
        print("Scipt Aplicado!")      
    end
})

-- Finalizando a interface
OrionLib:Init()
