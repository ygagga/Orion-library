local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()


local Window = OrionLib:MakeWindow({Name = "Teste", HidePremium = false, SaveConfig = true, ConfigFolder = "OrionTest"})


local TesteTab = Window:MakeTab({
    Name = "Teste",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local PlayerTab = Window:MakeTab({
    Name = "Jogadores",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})


TesteTab:AddSection({
    Name = "TesteTab"
})

TesteTab:AddToggle({
	Name = "This is a toggle!",
	Default = false,
	Callback = function(Value)
		game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100
	end    
})
