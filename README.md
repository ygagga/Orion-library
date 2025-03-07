local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

-- Criando a janela principal da interface
local Window = OrionLib:MakeWindow({
    Name = "Testando Troll Hub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TrollHubConfig"
})

-- Criando uma aba simples para testar
local TestTab = Window:MakeTab({
    Name = "Testar",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Adicionando uma seção simples na aba de teste
local TestSection = TestTab:AddSection({
    Name = "Funções de Teste"
})

TestSection:AddButton({
    Name = "Clique aqui para testar",
    Callback = function()
        print("Botão de teste pressionado!")
    end
})

-- Finalizando a interface
OrionLib:Init()
