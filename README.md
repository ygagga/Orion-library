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

local AdminTab = Window:MakeTab({
    Name = "Admin",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-----------------------------------------------------------
-- Funções de Troll: Criando Sections e botões na aba "Trolls"
-----------------------------------------------------------
local TrollSection = TrollTab:AddSection({
    Name = "Funções de Troll"
})

TrollSection:AddButton({
    Name = "Matar Jogador",
    Callback = function()
        -- Aqui você pode colocar a função que mata o jogador
        print("Jogador Morto!")
        -- Exemplo de função para matar um jogador (substitua pelo código real)
        -- game:GetService("Players").LocalPlayer.Character:BreakJoints()
    end
})

TrollSection:AddButton({
    Name = "Teleportar Jogador",
    Callback = function()
        -- Coloque aqui o código para teleportar um jogador
        print("Jogador Teleportado!")
        -- Exemplo de código para teleportar (substitua pelo código real)
        -- game:GetService("Players").LocalPlayer.Character:MoveTo(someLocation)
    end
})

TrollSection:AddButton({
    Name = "Copiar Skin de Jogador",
    Callback = function()
        -- Aqui você pode adicionar a função de copiar skin
        print("Skin Copiada!")
        -- Exemplo de código para copiar a skin
        -- local targetPlayer = game:GetService("Players"):GetPlayerByName("PlayerName")
        -- local targetCharacter = targetPlayer.Character
        -- game:GetService("Players").LocalPlayer.Character:ClearAllChildren()
        -- game:GetService("Players").LocalPlayer.Character:Clone() -- Clone da skin
    end
})

-----------------------------------------------------------
-- Funções de Admin: Criando Sections e botões na aba "Admin"
-----------------------------------------------------------
local AdminSection = AdminTab:AddSection({
    Name = "Funções de Admin"
})

AdminSection:AddButton({
    Name = "Banir Jogador",
    Callback = function()
        -- Coloque o código para banir um jogador
        print("Jogador Banido!")
        -- Exemplo de código para banir jogador (substitua pelo código real)
        -- game:GetService("Players"):GetPlayerByName("PlayerName"):Kick("Banido!")
    end
})

AdminSection:AddButton({
    Name = "Aplicar Ban Automático",
    Callback = function()
        -- Código para aplicar ban automático
        print("Ban Automático Aplicado!")
        -- Exemplo de código para aplicar ban automático (substitua com o código real)
        -- if game:GetService("Players"):GetPlayerByName("PlayerName") then
        --     game:GetService("Players"):GetPlayerByName("PlayerName"):Kick("Banido automaticamente!")
        -- end
    end
})

-- Finalizando a interface
OrionLib:Init()
