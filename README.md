local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

local Window = OrionLib:MakeWindow({
	Name = "XIAON'S HUB",
	HidePremium = false,
	SaveConfig = true,
	ConfigFolder = "OrionTest"
})

-- MAIN TAB
local MainTab = Window:MakeTab({
	Name = "ðŸ  Main",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

local MainSection = MainTab:AddSection({ Name = "Client" })

local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()

MainTab:AddSlider({
	Name = "Walkspeed",
	Min = 16,
	Max = 200,
	Default = 16,
	Color = Color3.fromRGB(255, 0, 0),
	Increment = 1,
	ValueName = "Speed",
	Callback = function(Value)
		if char:FindFirstChild("Humanoid") then
			char.Humanoid.WalkSpeed = Value
		end
	end    
})

MainTab:AddSlider({
	Name = "Jump Power",
	Min = 50,
	Max = 500,
	Default = 50,
	Color = Color3.fromRGB(0, 255, 0),
	Increment = 5,
	ValueName = "Power",
	Callback = function(Value)
		if char:FindFirstChild("Humanoid") then
			char.Humanoid.JumpPower = Value
		end
	end    
})

MainTab:AddToggle({
	Name = "Infinite Jump",
	Default = false,
	Callback = function(Value)
		if Value then
			game:GetService("UserInputService").JumpRequest:Connect(function()
				if char:FindFirstChild("Humanoid") then
					char.Humanoid:ChangeState("Jumping")
				end
			end)
		end
	end
})

MainTab:AddButton({
	Name = "Reset Character",
	Callback = function()
		char:BreakJoints()
	end    
})

-- ESP TAB
local ESPTab = Window:MakeTab({
	Name = "ðŸ” ESP",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

local ESPSection = ESPTab:AddSection({ Name = "Player ESP" })

local espColor = Color3.new(1, 0, 0)
local rainbowESP = false
local espActive = false

ESPTab:AddToggle({
	Name = "Enable ESP",
	Default = false,
	Callback = function(Value)
		espActive = Value
		if Value then
			spawn(function()
				while espActive do
					for _, player in ipairs(game.Players:GetPlayers()) do
						if player ~= game.Players.LocalPlayer and player.Character then
							if not player.Character:FindFirstChild("Highlight") then
								local esp = Instance.new("Highlight", player.Character)
								esp.FillTransparency = 0.5
								esp.OutlineTransparency = 0
							end
							if rainbowESP then
								espColor = Color3.fromHSV(tick() % 5 / 5, 1, 1)
							end
							for _, obj in ipairs(player.Character:GetChildren()) do
								if obj:IsA("Highlight") then
									obj.FillColor = espColor
								end
							end
						end
					end
					wait(0.1)
				end
			end)
		else
			for _, player in ipairs(game.Players:GetPlayers()) do
				if player.Character then
					for _, obj in ipairs(player.Character:GetChildren()) do
						if obj:IsA("Highlight") then
							obj:Destroy()
						end
					end
				end
			end
		end
	end    
})

ESPTab:AddToggle({
	Name = "Rainbow ESP",
	Default = false,
	Callback = function(Value)
		rainbowESP = Value
	end
})

ESPTab:AddColorPicker({
	Name = "ESP Color",
	Default = Color3.new(1, 0, 0),
	Callback = function(Value)
		espColor = Value
		rainbowESP = false
	end
})

-- SETTINGS TAB
local SettingsTab = Window:MakeTab({
	Name = "âš™ï¸ Settings",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

local SettingsSection = SettingsTab:AddSection({ Name = "Customization" })

SettingsTab:AddColorPicker({
	Name = "Menu Accent Color",
	Default = Color3.fromRGB(255, 0, 0),
	Callback = function(Value)
		Window:SetTheme("Accent", Value)
	end
})

SettingsTab:AddToggle({
	Name = "Enable Notifications",
	Default = true,
	Callback = function(Value)
		OrionLib:Set("Notifications", Value)
	end
})

SettingsTab:AddKeybind({
	Name = "Toggle UI",
	Default = Enum.KeyCode.RightShift,
	Hold = false,
	Callback = function()
		OrionLib:Toggle()
	end
})

-- FUN TAB
local FunTab = Window:MakeTab({
	Name = "ðŸŽ‰ Fun",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

local FunSection = FunTab:AddSection({ Name = "Player Fun" })

FunTab:AddButton({
	Name = "Spin Character",
	Callback = function()
		while true do
			char:SetPrimaryPartCFrame(char.PrimaryPart.CFrame * CFrame.Angles(0, math.rad(10), 0))
			wait(0.1)
		end
	end
})

FunTab:AddToggle({
	Name = "NoClip",
	Default = false,
	Callback = function(Value)
		game:GetService("RunService").Stepped:Connect(function()
			if Value then
				for _, part in ipairs(char:GetDescendants()) do
					if part:IsA("BasePart") then
						part.CanCollide = false
					end
				end
			end
		end)
	end
})
