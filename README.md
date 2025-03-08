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


PlayerTab:AddSection({
    Name = "TesteTab"
})


PlayerTab:AddSlider({

	Name = "WalkSpeed",

	Min = Lowest Speed,
	Max = Your Speed Maxed,
	Default = 5,
	Color = Color3.fromRGB(255,255,255),
	Increment = 1,
	ValueName = "WS",
	Callback = function(Value)
		game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
	end    
})

	Name = "jumppower",

	Min = Lowest Speed,
	Max = Your Speed Maxed,
	Default = 5,
	Color = Color3.fromRGB(255,255,255),
	Increment = 1,
	ValueName = "JP",
	Callback = function(Value)
		game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
	end   })
	
	
	TesteTab:AddSection({
    Name = "TesteTab"
})

Tab:AddSlider({

	Name = "Jump Height",

	Min = Lowest Speed,
	Max = Your Speed Maxed,
	Default = 5,
	Color = Color3.fromRGB(255,255,255),
	Increment = 1,
	ValueName = "Height",
	Callback = function(Value)
		game.Players.LocalPlayer.Character.Humanoid.JumpPower = Value
	end    
})


