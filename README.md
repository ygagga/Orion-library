local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

local Window = OrionLib:MakeWindow({
    Name = "Troll Hub", 
    HidePremium = false, 
    SaveConfig = true, 
    ConfigFolder = "TrollHubCfg", 
    IntroEnabled = false
})

local player = game.Players.LocalPlayer
local targetName = ""

-- Função para teleportar
local function TeleportToPlayer()
    local targetPlayer = game.Players:FindFirstChild(targetName)
    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        player.Character:WaitForChild("HumanoidRootPart").CFrame = targetPlayer.Character.HumanoidRootPart.CFrame
    else
        print("Jogador não encontrado!")
    end
end

-- Aba Player
local PlayerTab = Window:MakeTab({
    Name = "Player",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

PlayerTab:AddTextbox({
    Name = "Nome do Alvo",
    Default = "",
    TextDisappear = true,
    Callback = function(value)
        targetName = value
    end  
})

PlayerTab:AddButton({
    Name = "Teleportar",
    Callback = function()
        TeleportToPlayer()
    end  
})

OrionLib:Init()
