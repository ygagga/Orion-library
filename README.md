-- Carregar a Rayfield Library
local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

-- Criar a Janela Principal
local Window = Rayfield:CreateWindow({
   Name = "Troll Hub 🤡 | Brookhaven RP 🏡",
   LoadingTitle = "Carregando Troll Hub...",
   LoadingSubtitle = "Preparando ferramentas...",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = "TrollHub",
      FileName = "TrollHubSettings"
   },
   Discord = {
      Enabled = false,
      Invite = "", -- Pode adicionar um convite do Discord se quiser
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

-----------------------------------------------------------
-- 🎶 MÚSICA (Tocar ID de Música)
-----------------------------------------------------------
MusicTab:CreateSection("Reproduzir Música")

local musicId = ""
local loopMusic = false

MusicTab:CreateInput({
   Name = "ID da Música",
   PlaceholderText = "Digite o ID da música",
   RemoveTextAfterFocusLost = false,
   Callback = function(value)
      musicId = value
   end
})

MusicTab:CreateToggle({
   Name = "Loop",
   Default = false,
   Callback = function(value)
      loopMusic = value
   end
})

MusicTab:CreateButton({
   Name = "Reproduzir Música 🎶",
   Callback = function()
      if musicId ~= "" then
         local sound = Instance.new("Sound", game.Workspace)
         sound.SoundId = "rbxassetid://" .. musicId
         sound.Looped = loopMusic
         sound.Volume = 1
         sound:Play()
      end
   end
})

-----------------------------------------------------------
-- ⚡ HACKS (Super Velocidade e Pulo Infinito)
-----------------------------------------------------------
HacksTab:CreateSection("Superpoderes!")

HacksTab:CreateButton({
   Name = "Ativar Super Velocidade ⚡",
   Callback = function()
      game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100
   end
})

HacksTab:CreateButton({
   Name = "Desativar Velocidade ❌",
   Callback = function()
      game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
   end
})

HacksTab:CreateButton({
   Name = "Ativar Pulo Infinito 🦘",
   Callback = function()
      game:GetService("UserInputService").JumpRequest:Connect(function()
         game.Players.LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
      end)
   end
})

HacksTab:CreateButton({
   Name = "Desativar Pulo Infinito ❌",
   Callback = function()
      game:GetService("UserInputService").JumpRequest:Disconnect()
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
