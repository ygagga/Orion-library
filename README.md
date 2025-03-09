local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Teleport Hub",
   LoadingTitle = "Carregando...",
   LoadingSubtitle = "by SeuNome",
   Theme = "Default"
})

local TeleportTab = Window:CreateTab("Teleport", "globe") -- Ícone de globo

local Section = TeleportTab:CreateSection("Selecione um Jogador")

local SelectedPlayer

-- Função para obter a lista de jogadores
local function GetPlayers()
   local PlayersList = {}
   for _, player in ipairs(game:GetService("Players"):GetPlayers()) do
      if player ~= game.Players.LocalPlayer then -- Remove o próprio jogador da lista
         table.insert(PlayersList, player.Name)
      end
   end
   return PlayersList
end

-- Criando o dropdown de jogadores
local PlayerDropdown = TeleportTab:CreateDropdown({
   Name = "Jogadores",
   Options = GetPlayers(),
   CurrentOption = "",
   Callback = function(option)
      SelectedPlayer = option
   end
})

-- Criando o botão de teleporte
local TeleportButton = TeleportTab:CreateButton({
   Name = "Teleportar",
   Callback = function()
      local LocalPlayer = game.Players.LocalPlayer
      local TargetPlayer = game.Players:FindFirstChild(SelectedPlayer)

      if TargetPlayer and TargetPlayer.Character and TargetPlayer.Character:FindFirstChild("HumanoidRootPart") then
         LocalPlayer.Character:MoveTo(TargetPlayer.Character.HumanoidRootPart.Position)
         Rayfield:Notify({Title = "Sucesso", Content = "Teleportado para "..SelectedPlayer, Duration = 2})
      else
         Rayfield:Notify({Title = "Erro", Content = "Jogador inválido ou sem personagem", Duration = 2})
      end
   end
})

-- Criando um botão para atualizar a lista de jogadores
local RefreshButton = TeleportTab:CreateButton({
   Name = "Atualizar Lista",
   Callback = function()
      PlayerDropdown:Set(GetPlayers())
      Rayfield:Notify({Title = "Atualizado", Content = "Lista de jogadores atualizada", Duration = 2})
   end
})
