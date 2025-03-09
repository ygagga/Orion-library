local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Teleport Hub",
   LoadingTitle = "Carregando...",
   LoadingSubtitle = "by SeuNome",
   Theme = "Default"
})

local TeleportTab = Window:CreateTab("Teleport", "globe") -- Ícone de globo

local Section = TeleportTab:CreateSection("Selecione um Jogador")

local PlayersList = {} 
for _, player in ipairs(game:GetService("Players"):GetPlayers()) do
   table.insert(PlayersList, player.Name)
end

local SelectedPlayer

local PlayerDropdown = TeleportTab:CreateDropdown({
   Name = "Jogadores",
   Options = PlayersList,
   CurrentOption = "",
   Callback = function(option)
      SelectedPlayer = option
   end
})

local TeleportButton = TeleportTab:CreateButton({
   Name = "Teleportar",
   Callback = function()
      local LocalPlayer = game.Players.LocalPlayer
      local TargetPlayer = game.Players:FindFirstChild(SelectedPlayer)

      if TargetPlayer and TargetPlayer.Character and LocalPlayer.Character then
         LocalPlayer.Character:MoveTo(TargetPlayer.Character:GetPrimaryPartCFrame().Position)
         Rayfield:Notify({Title = "Sucesso", Content = "Teleportado para "..SelectedPlayer, Duration = 2})
      else
         Rayfield:Notify({Title = "Erro", Content = "Jogador inválido", Duration = 2})
      end
   end
})
