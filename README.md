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

PlayerTab:AddButton({
	Name = "ESP (Q to toggle on and off)",
	Callback = function()
      	loadstring(game:HttpGet("https://raw.githubusercontent.com/Exunys/ESP-Script/main/ESP.lua"))()
  	end    
})


PlayerTab:AddButton({
	Name = "Fling",
	Callback = function()
	    loadstring(game:HttpGet(('https://raw.githubusercontent.com/0Ben1/fe/main/obf_5wpM7bBcOPspmX7lQ3m75SrYNWqxZ858ai3tJdEAId6jSI05IOUB224FQ0VSAswH.lua.txt'),true))()
  	end    
})
