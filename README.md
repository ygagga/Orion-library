local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

local Window = OrionLib:MakeWindow({Name = "Troll Hub", HidePremium = false, SaveConfig = true, ConfigFolder = "TrollHubCfg", IntroEnabled = false})

-- Variáveis globais
local player = game.Players.LocalPlayer
local targetPlayer = nil

-- Funções de Troll

-- Teleportar para o alvo
local function ForceTP(targetName)
    targetPlayer = game.Players:FindFirstChild(targetName)
    if targetPlayer then
        player.Character:SetPrimaryPartCFrame(targetPlayer.Character.HumanoidRootPart.CFrame)
    else
        print("Jogador não encontrado!")
    end
end

-- Matar jogador com carro
local function KillPlayerWithCar(targetName)
    targetPlayer = game.Players:FindFirstChild(targetName)
    if targetPlayer then
        -- Cria um carro ou usa um existente, ajustando a lógica conforme necessário
        local car = Instance.new("VehicleSeat")
        car.Parent = workspace
        car.CFrame = targetPlayer.Character.HumanoidRootPart.CFrame
        targetPlayer.Character:BreakJoints()
        print(targetName .. " foi morto com o carro!")
    else
        print("Jogador não encontrado!")
    end
end

-- Copiar a skin de outro jogador
local function CopyPlayerSkin(targetName)
    targetPlayer = game.Players:FindFirstChild(targetName)
    if targetPlayer then
        -- Copiar as partes do personagem, como roupas e acessórios
        player.CharacterAppearance = targetPlayer.CharacterAppearance
        print("Skin de " .. targetName .. " copiada com sucesso!")
    else
        print("Jogador não encontrado!")
    end
end

-- Spawnar um sofá e matar o jogador
local function SpawnSofaAndKill(targetName)
    targetPlayer = game.Players:FindFirstChild(targetName)
    if targetPlayer then
        -- Criando um sofá e teleportando o jogador para o void
        local sofa = Instance.new("Part")
        sofa.Size = Vector3.new(4, 1, 4)
        sofa.Shape = Enum.PartType.Ball
        sofa.Anchored = true
        sofa.Parent = workspace
        sofa.CFrame = targetPlayer.Character.HumanoidRootPart.CFrame

        -- Teleportando para o void
        wait(2)
        targetPlayer.Character:SetPrimaryPartCFrame(CFrame.new(0, -1000, 0))  -- Teleporta para o void
        wait(1)
        targetPlayer.Character:BreakJoints()  -- Mata o jogador
        print(targetName .. " foi morto com o sofá!")
    else
        print("Jogador não encontrado!")
    end
end

-- Abas e Botões

local PlayerTab = Window:MakeTab({
    Name = "Trolls",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local Section = PlayerTab:AddSection({
    Name = "Ações de Troll"
})

-- Adicionando botões para as ações de troll

PlayerTab:AddTextbox({
    Name = "Nome do Alvo",
    Default = "NomeDoJogador",
    TextDisappear = true,
    Callback = function(value)
        targetPlayer = game.Players:FindFirstChild(value)
        if not targetPlayer then
            print("Jogador não encontrado!")
        end
    end  
})

PlayerTab:AddButton({
    Name = "Force TP",
    Callback = function()
        if targetPlayer then
            ForceTP(targetPlayer.Name)
        else
            print("Nenhum alvo selecionado!")
        end
    end  
})

PlayerTab:AddButton({
    Name = "Matar com Carro",
    Callback = function()
        if targetPlayer then
            KillPlayerWithCar(targetPlayer.Name)
        else
            print("Nenhum alvo selecionado!")
        end
    end  
})

PlayerTab:AddButton({
    Name = "Copiar Skin",
    Callback = function()
        if targetPlayer then
            CopyPlayerSkin(targetPlayer.Name)
        else
            print("Nenhum alvo selecionado!")
        end
    end  
})

PlayerTab:AddButton({
    Name = "Spawn Sofa e Matar",
    Callback = function()
        if targetPlayer then
            SpawnSofaAndKill(targetPlayer.Name)
        else
            print("Nenhum alvo selecionado!")
        end
    end  
})

-- Inicializando a interface
OrionLib:Init()
