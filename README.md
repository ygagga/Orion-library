-- Carregar a Rayfield Library
local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

-- Criar a Janela Principal
local Window = Rayfield:CreateWindow({
   Name = "👾ZenithCore👾 | Brookhaven RP 🏡",
   LoadingTitle = "Carregando Zenith Core...",
   LoadingSubtitle = "Preparando ferramentas...",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = "Rayfield",
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
