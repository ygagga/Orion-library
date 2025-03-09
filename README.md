-- Carregar a Rayfield Library
local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

-- Criar a Janela Principal
local Window = Rayfield:CreateWindow({
   Name = "👾ZenithCore👾 | Brookhaven RP 🏡",
   LoadingTitle = "Carregando Troll Hub...",
   LoadingSubtitle = "Preparando ferramentas...",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = "Zenith Core",
      FileName = "TrollHubSettings"
   },
   Discord = {
      Enabled = false,
      Invite = "https://discord.gg/A269Qwmq",
      RememberJoins = true
   },
   KeySystem = false
})

-- Criar as Abas (Tabs)
local TrollTab = Window:CreateTab("Troll", 4483362458) -- Ícone de palhaço
local MusicTab = Window:CreateTab("Música", 6034509993) -- Ícone de música
local HacksTab = Window:CreateTab("Hacks", 6034509993) -- Ícone de raio
local ScriptsTab = Window:CreateTab("Scripts", 6034509973) -- Ícone de código
local AboutTab = Window:CreateTab("Sobre", 6034509992) -- Ícone de info

-----------------------------------------------------------
-- 🤡 TROLL (Teleportar, Espectar, Matar)
-----------------------------------------------------------
TrollTab:CreateSection("Controle de Jogadores")

local selectedPlayer = ""

TrollTab:CreateInput({
   Name = "Nome do Jogador",
   PlaceholderText = "Digite o nome do jogador",
   RemoveTextAfterFocusLost = true,
   Callback = function(value)
      selectedPlayer = value
   end
})

TrollTab:CreateButton({
   Name = "Teleportar Todos para Mim",
   Callback = function()
      local players = game:GetService("Players")
      local localPlayer = players.LocalPlayer
      local root = localPlayer.Character and localPlayer.Character:FindFirstChild("HumanoidRootPart")

      if root then
         for _, target in pairs(players:GetPlayers()) do
            if target.Character and target ~= localPlayer then
               local targetRoot = target.Character:FindFirstChild("HumanoidRootPart")
               if targetRoot then
                  targetRoot.CFrame = root.CFrame
               end
            end
         end
      end
   end
})

TrollTab:CreateButton({
   Name = "Espectar Jogador",
   Callback = function()
      local players = game:GetService("Players")
      local target = players:FindFirstChild(selectedPlayer)

      if target and target.Character then
         game.Workspace.CurrentCamera.CameraSubject = target.Character:FindFirstChildOfClass("Humanoid")
      end
   end
})

TrollTab:CreateButton({
   Name = "Parar de Espectar",
   Callback = function()
      game.Workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
   end
})


--------------------------------------
-- 🎶 Aba Música (Tocar para Todos)
--------------------------------------

MusicTab:CreateSection("Escolha sua Música")

local globalMusicId = ""
local globalSound
local isLoopEnabled = false  -- Toggle para loop

-- Toggle para ativar/desativar loop
MusicTab:CreateToggle({
    Name = "Tocar em Loop 🔁",
    CurrentValue = false,
    Callback = function(value)
        isLoopEnabled = value
    end
})

-- Campo para inserir ID da música global
MusicTab:CreateInput({
    Name = "ID da Música Global",
    PlaceholderText = "Digite o ID...",
    RemoveTextAfterFocusLost = false,
    Callback = function(value)
        globalMusicId = value
    end
})

-- IDs prontos para facilitar
local musicIds = {
    ["🎵 Música 1"] = "6454199333",
    ["🎵 Música 2"] = "6427245762",
    ["🎵 Música 3"] = "6489326185",
    ["🎵 Música 4"] = "6433157341",
    ["🎵 Música 5"] = "6436089393",
    ["🎵 Música 6"] = "18841894272",
    ["🎵 Música 7"] = "16190784547"
}

-- Criar botões para tocar músicas prontas globalmente
for name, id in pairs(musicIds) do
    MusicTab:CreateButton({
        Name = name,
        Callback = function()
            if globalSound then globalSound:Destroy() end
            globalSound = Instance.new("Sound", game.Workspace)
            globalSound.SoundId = "rbxassetid://" .. id
            globalSound.Volume = 10
            globalSound.Looped = isLoopEnabled  -- Aplica a escolha do loop
            globalSound:Play()
        end
    })
end

-- Botão para tocar a música globalmente com ID personalizado
MusicTab:CreateButton({
    Name = "Tocar ID Personalizado 📢",
    Callback = function()
        if globalMusicId ~= "" then
            if globalSound then globalSound:Destroy() end
            globalSound = Instance.new("Sound", game.Workspace)
            globalSound.SoundId = "rbxassetid://" .. globalMusicId
            globalSound.Volume = 10
            globalSound.Looped = isLoopEnabled  -- Aplica a escolha do loop
            globalSound:Play()
        end
    end
})

-- Botão para parar a música global
MusicTab:CreateButton({
    Name = "Parar Música Global ⛔",
    Callback = function()
        if globalSound then
            globalSound:Stop()
            globalSound:Destroy()
            globalSound = nil
        end
    end
})


--------------------------------------
-- ⚡ ESP (Ver Jogadores + Distância)
--------------------------------------

HacksTab:CreateSection("ESP - Ver Jogadores")

local espEnabled = false
local espObjects = {}

local function createESP(player)
    if player == game.Players.LocalPlayer then return end
    if not player.Character then return end

    -- Criar Highlight para ESP
    local highlight = Instance.new("Highlight")
    highlight.Parent = player.Character
    highlight.FillColor = Color3.fromRGB(255, 255, 255) -- Branco
    highlight.FillTransparency = 0.5
    highlight.OutlineTransparency = 0.1

    -- Criar BillboardGui para mostrar a distância
    local billboard = Instance.new("BillboardGui")
    billboard.Parent = player.Character:FindFirstChild("Head") or player.Character.PrimaryPart
    billboard.Adornee = player.Character:FindFirstChild("Head") or player.Character.PrimaryPart
    billboard.Size = UDim2.new(0, 100, 0, 50)
    billboard.StudsOffset = Vector3.new(0, 2, 0)

    local textLabel = Instance.new("TextLabel")
    textLabel.Parent = billboard
    textLabel.Size = UDim2.new(1, 0, 1, 0)
    textLabel.BackgroundTransparency = 1
    textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    textLabel.TextStrokeTransparency = 0
    textLabel.TextScaled = true
    textLabel.Font = Enum.Font.SourceSansBold

    espObjects[player] = {highlight, billboard, textLabel}

    -- Atualizar a distância
    task.spawn(function()
        while espEnabled and player.Character and player.Character.PrimaryPart do
            local distance = (game.Players.LocalPlayer.Character.PrimaryPart.Position - player.Character.PrimaryPart.Position).Magnitude
            textLabel.Text = string.format("📍 %d Studs", math.floor(distance))
            task.wait(0.1)
        end
    end)
end

-- Ativar ESP
HacksTab:CreateToggle({
    Name = "Ativar ESP 👁️",
    CurrentValue = false,
    Callback = function(value)
        espEnabled = value

        if espEnabled then
            for _, player in pairs(game.Players:GetPlayers()) do
                createESP(player)
            end

            -- Atualizar ESP quando novos jogadores entrarem
            game.Players.PlayerAdded:Connect(createESP)
        else
            -- Remover ESP
            for _, objects in pairs(espObjects) do
                if objects[1] then objects[1]:Destroy() end
                if objects[2] then objects[2]:Destroy() end
            end
            espObjects = {}
        end
    end
})


-----------------------------------------------------------
-- 🧑‍💻 SCRIPTS (Executar Scripts Extras)
-----------------------------------------------------------
ScriptsTab:CreateSection("Executar Scripts")

ScriptsTab:CreateButton({
   Name = "Fly Script ✈️",
   Callback = function()
      loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()
   end
})

ScriptsTab:CreateButton({
   Name = "RAEL Hub 🔧",
   Callback = function()
      loadstring(game:HttpGet("https://raw.githubusercontent.com/Laelmano24/Rael-Hub/main/main.txt"))()
   end
})

ScriptsTab:CreateButton({
   Name = "Sander X 🛸",
   Callback = function()
      loadstring(game:HttpGet('https://raw.githubusercontent.com/sXPiterXs1111/Sanderxv3.30/main/sanderx3.30'))()
   end
})

-----------------------------------------------------------
-- ℹ️ SOBRE
-----------------------------------------------------------
AboutTab:CreateSection("Criado por Shelby, user discord: snobodj")

AboutTab:CreateParagraph({
   Title = "Troll Hub 🤡",
   Content = "Criado para trollar no Brookhaven RP! Divirta-se!"
})

Rayfield:LoadConfiguration()
