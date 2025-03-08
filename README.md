local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()
local Fluent = loadstring(game:HttpGet('https://raw.githubusercontent.com/FluentHD/Fluent/main/Fluent.lua'))()

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

-- Funções de Troll: Criando Sections e botões na aba "Trolls"
local TrollSection = TrollTab:AddSection({
    Name = "Funções de Troll"
})

TrollSection:AddButton({
    Name = "Matar Jogador",
    Callback = function()
        -- Função para matar jogador
        local player = game.Players.LocalPlayer
        player.Character:BreakJoints()
        print("Jogador Morto!")
    end
})

TrollSection:AddButton({
    Name = "Teleportar Jogador",
    Callback = function()
        -- Função para teleportar o jogador selecionado
        local targetPlayer = game.Players:FindFirstChild("JogadorAlvo")  -- Substitua "JogadorAlvo" pelo nome do jogador
        if targetPlayer then
            targetPlayer.Character:SetPrimaryPartCFrame(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
            print("Jogador Teleportado!")
        else
            print("Jogador não encontrado!")
        end
    end
})

TrollSection:AddButton({
    Name = "Copiar Skin de Jogador",
    Callback = function()
        -- Função para copiar a skin de um jogador
        local targetPlayer = game.Players:FindFirstChild("JogadorAlvo")  -- Substitua "JogadorAlvo" pelo nome do jogador
        if targetPlayer and targetPlayer.Character then
            local targetCharacter = targetPlayer.Character
            game.Players.LocalPlayer.Character:ClearAllChildren()
            targetCharacter:Clone().Parent = game.Players.LocalPlayer.Character
            print("Skin Copiada!")
        else
            print("Jogador não encontrado!")
        end
    end
})

-- Funções de Admin: Criando Sections e botões na aba "Admin"
local AdminSection = AdminTab:AddSection({
    Name = "Funções de Admin"
})

AdminSection:AddButton({
    Name = "Banir Jogador",
    Callback = function()
        -- Função para banir o jogador
        local targetPlayer = game.Players:FindFirstChild("JogadorAlvo")  -- Substitua "JogadorAlvo" pelo nome do jogador
        if targetPlayer then
            targetPlayer:Kick("Banido!")
            print("Jogador Banido!")
        else
            print("Jogador não encontrado!")
        end
    end
})

AdminSection:AddButton({
    Name = "Aplicar Ban Automático",
    Callback = function()
        -- Função para aplicar ban automático
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Name == "JogadorAlvo" then  -- Substitua "JogadorAlvo" pelo nome do jogador alvo
                player:Kick("Banido automaticamente!")
                print("Ban Automático Aplicado!")
                break
            end
        end
    end
})

-- Criando uma janela Fluent para interagir com o player
local fluentWindow = Fluent:CreateWindow({
    Name = "Funções de Troll",
    Size = UDim2.new(0, 400, 0, 250),
    Position = UDim2.new(0.5, -200, 0.5, -125)
})

local fluentTrollTab = fluentWindow:AddTab("Trolls")
local fluentAdminTab = fluentWindow:AddTab("Admin")

-- Funções de Troll na Fluent
fluentTrollTab:AddButton("Matar Jogador", function()
    local player = game.Players.LocalPlayer
    player.Character:BreakJoints()
    print("Jogador Morto!")
end)

fluentTrollTab:AddButton("Teleportar Jogador", function()
    local targetPlayer = game.Players:FindFirstChild("JogadorAlvo")  -- Substitua "JogadorAlvo" pelo nome do jogador
    if targetPlayer then
        targetPlayer.Character:SetPrimaryPartCFrame(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
        print("Jogador Teleportado!")
    else
        print("Jogador não encontrado!")
    end
end)

fluentTrollTab:AddButton("test", function()
    local player = game.Players.LocalPlayer
local camera = game.Workspace.CurrentCamera

-- Função para calcular a distância
local function getDistance(playerPosition, targetPosition)
    return (playerPosition - targetPosition).Magnitude
end

-- Função para desenhar o ESP
local function drawESP(target)
    -- Garantir que o jogador tem uma parte "HumanoidRootPart"
    if not target.Character or not target.Character:FindFirstChild("HumanoidRootPart") then return end

    local distance = getDistance(player.Character.HumanoidRootPart.Position, target.Character.HumanoidRootPart.Position)
    local screenPosition, onScreen = camera:WorldToScreenPoint(target.Character.HumanoidRootPart.Position)

    -- Se o jogador estiver na tela
    if onScreen then
        -- Criando a caixa de ESP (verde e fixada)
        local box = Instance.new("Frame")
        box.Parent = game.CoreGui
        box.Size = UDim2.new(0, 50, 0, 50)  -- Tamanho da caixa (pode ajustar)
        box.Position = UDim2.new(0, screenPosition.X - 25, 0, screenPosition.Y - 25)  -- Posição da caixa
        box.BackgroundColor3 = Color3.fromRGB(0, 255, 0)  -- Cor da caixa (verde)
        box.BorderSizePixel = 2

        -- Exibindo a distância na caixa
        local distanceLabel = Instance.new("TextLabel")
        distanceLabel.Parent = box
        distanceLabel.Size = UDim2.new(1, 0, 1, 0)
        distanceLabel.Text = math.floor(distance) .. "m"  -- Mostra a distância em metros
        distanceLabel.TextColor3 = Color3.fromRGB(255, 255, 255)  -- Cor do texto (branco)
        distanceLabel.BackgroundTransparency = 1  -- Sem fundo para o texto

        -- Atualizar a posição da caixa e distância a cada segundo
        game:GetService("RunService").Heartbeat:Connect(function()
            local newScreenPosition, onScreenAgain = camera:WorldToScreenPoint(target.Character.HumanoidRootPart.Position)
            if onScreenAgain then
                box.Position = UDim2.new(0, newScreenPosition.X - 25, 0, newScreenPosition.Y - 25)
                distanceLabel.Text = math.floor(getDistance(player.Character.HumanoidRootPart.Position, target.Character.HumanoidRootPart.Position)) .. "m"
            end
        end)
    end
end

-- Monitorando todos os jogadores
game:GetService("RunService").RenderStepped:Connect(function()
    for _, target in ipairs(game.Players:GetPlayers()) do
        -- Ignorando o jogador que executa o script
        if target ~= player then
            drawESP(target)
        end
    end
end)
        print("Esp Ativado!")
    else
        print("Jogador não encontrado!")
    end
end)

-- Funções de Admin na Fluent
fluentAdminTab:AddButton("Banir Jogador", function()
    local targetPlayer = game.Players:FindFirstChild("JogadorAlvo")  -- Substitua "JogadorAlvo" pelo nome do jogador
    if targetPlayer then
        targetPlayer:Kick("Banido!")
        print("Jogador Banido!")
    else
        print("Jogador não encontrado!")
    end
end)

fluentAdminTab:AddButton("Aplicar Ban Automático", function()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player.Name == "JogadorAlvo" then  -- Substitua "JogadorAlvo" pelo nome do jogador alvo
            player:Kick("Banido automaticamente!")
            print("Ban Automático Aplicado!")
            break
        end
    end
end)

-- Finalizando a interface
OrionLib:Init()
fluentWindow:Show()
