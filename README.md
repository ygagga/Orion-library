-- Código otimizado da biblioteca OrionLib

-- Serviços local Services = { UserInputService = game:GetService("UserInputService"), TweenService = game:GetService("TweenService"), RunService = game:GetService("RunService"), Players = game:GetService("Players"), HttpService = game:GetService("HttpService") }

local LocalPlayer = Services.Players.LocalPlayer local Mouse = LocalPlayer:GetMouse()

-- OrionLib local OrionLib = { Elements = {}, ThemeObjects = {}, Connections = {}, Flags = {}, Themes = { Default = { Main = Color3.fromRGB(25, 25, 25), Second = Color3.fromRGB(32, 32, 32), Stroke = Color3.fromRGB(60, 60, 60), Divider = Color3.fromRGB(60, 60, 60), Text = Color3.fromRGB(240, 240, 240), TextDark = Color3.fromRGB(150, 150, 150) } }, SelectedTheme = "Default", Folder = nil, SaveCfg = false }

-- Feather Icons local Icons = {} local success, result = pcall(function() Icons = Services.HttpService:JSONDecode(game:HttpGet("https://raw.githubusercontent.com/evoincorp/lucideblox/master/src/modules/util/icons.json")).icons end) if not success then warn("Orion Library - Failed to load icons: " .. result) end local function GetIcon(name) return Icons[name] end

-- GUI principal local Orion = Instance.new("ScreenGui") Orion.Name = "Orion" if syn then syn.protect_gui(Orion) end Orion.Parent = gethui and gethui() or game.CoreGui

-- Remover interfaces duplicadas local function RemoveDuplicates() local parent = gethui and gethui() or game.CoreGui for _, ui in ipairs(parent:GetChildren()) do if ui.Name == Orion.Name and ui ~= Orion then ui:Destroy() end end end RemoveDuplicates()

function OrionLib:IsRunning() return Orion.Parent == (gethui and gethui() or game.CoreGui) end

-- Conexões local function AddConnection(signal, func) if not OrionLib:IsRunning() then return end local connection = signal:Connect(func) table.insert(OrionLib.Connections, connection) return connection end

-- Finalizar conexões ao encerrar Services.RunService.Heartbeat:Connect(function() if not OrionLib:IsRunning() then for _, conn in pairs(OrionLib.Connections) do conn:Disconnect() end end end)

-- Função de arrastar local function EnableDragging(dragPoint, mainFrame) local dragging, dragInput, startPos, framePos = false dragPoint.InputBegan:Connect(function(input) if input.UserInputType == Enum.UserInputType.MouseButton1 then dragging = true startPos, framePos = input.Position, mainFrame.Position input.Changed:Connect(function() if input.UserInputState == Enum.UserInputState.End then dragging = false end end) end end) dragPoint.InputChanged:Connect(function(input) if input.UserInputType == Enum.UserInputType.MouseMovement then dragInput = input end end) Services.UserInputService.InputChanged:Connect(function(input) if input == dragInput and dragging then local delta = input.Position - startPos Services.TweenService:Create(mainFrame, TweenInfo.new(0.45, Enum.EasingStyle.Quint, Enum.EasingDirection.Out), { Position = UDim2.new(framePos.X.Scale, framePos.X.Offset + delta.X, framePos.Y.Scale, framePos.Y.Offset + delta.Y) }):Play() end end) end

-- Utilitários local function Create(class, props, children) local obj = Instance.new(class) for k, v in pairs(props or {}) do obj[k] = v end for _, child in pairs(children or {}) do child.Parent = obj end return obj end

local function AddThemeObject(obj, themeKey) OrionLib.ThemeObjects[themeKey] = OrionLib.ThemeObjects[themeKey] or {} table.insert(OrionLib.ThemeObjects[themeKey], obj) obj[ReturnProperty(obj)] = OrionLib.Themes[OrionLib.SelectedTheme][themeKey] return obj end

local function ReturnProperty(obj) local class = obj.ClassName return class == "Frame" or class == "TextButton" and "BackgroundColor3" or class == "ScrollingFrame" and "ScrollBarImageColor3" or class == "UIStroke" and "Color" or (class == "TextLabel" or class == "TextBox") and "TextColor3" or (class == "ImageLabel" or class == "ImageButton") and "ImageColor3" end

-- ORION LIBRARY OTIMIZADA POR RONALDO - VERSÃO REDZ/RAYFIELD STYLE
local Orion = {}

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

-- Armazena janelas criadas
local Windows = {}

-- Função para criar uma nova janela
function Orion:MakeWindow(cfg)
	local name = cfg.Name or "Orion Hub"
	local theme = cfg.Theme or "Dark"
	local size = cfg.Size or UDim2.new(0, 500, 0, 350)

	local ScreenGui = Instance.new("ScreenGui", PlayerGui)
	ScreenGui.Name = name:gsub("%s+", "") .. "UI"
	ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	ScreenGui.ResetOnSpawn = false

	local MainFrame = Instance.new("Frame", ScreenGui)
	MainFrame.Name = "Main"
	MainFrame.Size = size
	MainFrame.Position = UDim2.new(0.5, -size.X.Offset / 2, 0.5, -size.Y.Offset / 2)
	MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
	MainFrame.BorderSizePixel = 0
	MainFrame.AnchorPoint = Vector2.new(0.5, 0.5)

	local UIStroke = Instance.new("UIStroke", MainFrame)
	UIStroke.Color = Color3.fromRGB(255, 0, 0)
	UIStroke.Thickness = 2

	local UICorner = Instance.new("UICorner", MainFrame)
	UICorner.CornerRadius = UDim.new(0, 6)

	-- Título da janela
	local Title = Instance.new("TextLabel", MainFrame)
	Title.Text = name
	Title.Size = UDim2.new(1, 0, 0, 40)
	Title.BackgroundTransparency = 1
	Title.TextColor3 = Color3.fromRGB(255, 255, 255)
	Title.TextScaled = true
	Title.Font = Enum.Font.GothamBold

	-- Aba container
	local TabsHolder = Instance.new("Frame", MainFrame)
	TabsHolder.Name = "Tabs"
	TabsHolder.Position = UDim2.new(0, 0, 0, 40)
	TabsHolder.Size = UDim2.new(1, 0, 1, -40)
	TabsHolder.BackgroundTransparency = 1

	-- Layout de abas
	local UIList = Instance.new("UIListLayout", TabsHolder)
	UIList.FillDirection = Enum.FillDirection.Horizontal
	UIList.SortOrder = Enum.SortOrder.LayoutOrder
	UIList.Padding = UDim.new(0, 4)

	-- Armazena funções para manipular a janela
	local WindowAPI = {}

	function WindowAPI:CreateTab(tabName)
		local Tab = Instance.new("TextButton", TabsHolder)
		Tab.Name = tabName
		Tab.Text = tabName
		Tab.Size = UDim2.new(0, 100, 0, 30)
		Tab.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
		Tab.TextColor3 = Color3.fromRGB(255, 255, 255)
		Tab.Font = Enum.Font.Gotham
		Tab.TextScaled = true

		local TabCorner = Instance.new("UICorner", Tab)
		TabCorner.CornerRadius = UDim.new(0, 4)

		local Page = Instance.new("ScrollingFrame", MainFrame)
		Page.Name = tabName .. "Page"
		Page.Size = UDim2.new(1, -10, 1, -80)
		Page.Position = UDim2.new(0, 5, 0, 75)
		Page.BackgroundTransparency = 1
		Page.Visible = false
		Page.AutomaticCanvasSize = Enum.AutomaticSize.Y
		Page.CanvasSize = UDim2.new(0, 0, 0, 0)
		Page.ScrollBarThickness = 5

		local ListLayout = Instance.new("UIListLayout", Page)
		ListLayout.Padding = UDim.new(0, 6)
		ListLayout.SortOrder = Enum.SortOrder.LayoutOrder

		-- Trocar de aba
		Tab.MouseButton1Click:Connect(function()
			for _, child in pairs(MainFrame:GetChildren()) do
				if child:IsA("ScrollingFrame") then
					child.Visible = false
				end
			end
			Page.Visible = true
		end)

		local TabAPI = {}

		function TabAPI:AddLabel(text)
			local Label = Instance.new("TextLabel", Page)
			Label.Text = text
			Label.Size = UDim2.new(1, -10, 0, 30)
			Label.BackgroundTransparency = 1
			Label.TextColor3 = Color3.fromRGB(255, 255, 255)
			Label.Font = Enum.Font.GothamSemibold
			Label.TextScaled = true
		end

		function TabAPI:AddButton(text, callback)
			local Button = Instance.new("TextButton", Page)
			Button.Text = text
			Button.Size = UDim2.new(1, -10, 0, 35)
			Button.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
			Button.TextColor3 = Color3.fromRGB(255, 255, 255)
			Button.Font = Enum.Font.GothamBold
			Button.TextScaled = true

			local Corner = Instance.new("UICorner", Button)
			Corner.CornerRadius = UDim.new(0, 6)

			Button.MouseButton1Click:Connect(function()
				pcall(callback)
			end)
		end

		function TabAPI:AddToggle(text, callback)
			local Toggle = Instance.new("TextButton", Page)
			Toggle.Text = text .. " [OFF]"
			Toggle.Size = UDim2.new(1, -10, 0, 35)
			Toggle.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
			Toggle.TextColor3 = Color3.fromRGB(255, 255, 255)
			Toggle.Font = Enum.Font.Gotham
			Toggle.TextScaled = true

			local Corner = Instance.new("UICorner", Toggle)
			Corner.CornerRadius = UDim.new(0, 6)

			local state = false

			Toggle.MouseButton1Click:Connect(function()
				state = not state
				Toggle.Text = text .. (state and " [ON]" or " [OFF]")
				pcall(callback, state)
			end)
		end

		return TabAPI
	end

	return WindowAPI
end

return Orion
