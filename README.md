local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()
local Window = OrionLib:MakeWindow({Name = "DeadlyHub", HidePremium = True, IntroEnabled = true,IntroText = "DeadlyHub",IntroIcon = nil, SaveConfig = true, ConfigFolder = "DeadlyHubRoblox"})

--MainTab
local MainTab = Window:MakeTab({
	Name = "Main",
	Icon = nil,
	PremiumOnly = false
})

MainTab:AddButton({
	Name = "ESP (Q to toggle on and off)",
	Callback = function()
      	loadstring(game:HttpGet("https://raw.githubusercontent.com/Exunys/ESP-Script/main/ESP.lua"))()
  	end    
})

MainTab:AddButton({
	Name = "Fling",
	Callback = function()
	    loadstring(game:HttpGet(('https://raw.githubusercontent.com/0Ben1/fe/main/obf_5wpM7bBcOPspmX7lQ3m75SrYNWqxZ858ai3tJdEAId6jSI05IOUB224FQ0VSAswH.lua.txt'),true))()
  	end    
})



MainTab:AddButton({
	Name = "Noclip",
	Callback = function()
      		local player = game.Players.LocalPlayer
local mouse = player:GetMouse()
local runservice = game:GetService("RunService")
local noclip = false

local msg = Instance.new("Message", player.PlayerGui)
msg.Text = "Noclip Script! Press on 'e' to noclip & 't' to destroy this message!"

runservice.Stepped:Connect(function()
    if noclip then
        player.Character.Humanoid:ChangeState(11)
    end
end)

mouse.KeyDown:Connect(function(key)
    if key == "t" then
        msg:Destroy()
    end
end)

mouse.KeyDown:Connect(function(key)
    if key == "e" then
	    noclip = true
	    player.Character.Humanoid:ChangeState(11)
    end
end)
  	end    
})



MainTab:AddButton({
	Name = "Fly",
	Callback = function()
      		--Mobile Fly Script
        loadstring("\108\111\97\100\115\116\114\105\110\103\40\103\97\109\101\58\72\116\116\112\71\101\116\40\40\39\104\116\116\112\115\58\47\47\103\105\115\116\46\103\105\116\104\117\98\117\115\101\114\99\111\110\116\101\110\116\46\99\111\109\47\109\101\111\122\111\110\101\89\84\47\98\102\48\51\55\100\102\102\57\102\48\97\55\48\48\49\55\51\48\52\100\100\100\54\55\102\100\99\100\51\55\48\47\114\97\119\47\101\49\52\101\55\52\102\52\50\53\98\48\54\48\100\102\53\50\51\51\52\51\99\102\51\48\98\55\56\55\48\55\52\101\98\51\99\53\100\50\47\97\114\99\101\117\115\37\50\53\50\48\120\37\50\53\50\48\102\108\121\37\50\53\50\48\50\37\50\53\50\48\111\98\102\108\117\99\97\116\111\114\39\41\44\116\114\117\101\41\41\40\41\10\10")()
  	end    
})

MainTab:AddButton({
	Name = "Btools",
	Callback = function()
      	    loadstring(game:HttpGet("https://raw.githubusercontent.com/HeyGyt/btools/main/main"))()
  	end    
})
MainTab:AddButton({
	Name = "X-ray (Press E to active/disable)",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/HeyGyt/xray/main/main"))()
  	end    
})

MainTab:AddButton({
	Name = "FullBright",
	Callback = function()
      		game:GetService("Lighting").Brightness = 2
            game:GetService("Lighting").ClockTime = 14
            game:GetService("Lighting").FogEnd = 100000
            game:GetService("Lighting").GlobalShadows = false
            game:GetService("Lighting").OutdoorAmbient = Color3.fromRGB(128, 128, 128)
  	end    
})



MainTab:AddButton({
	Name = "Infinite Jump",
	Callback = function()
      		 loadstring(game:HttpGet("https://raw.githubusercontent.com/HeyGyt/infjump/main/main"))()
  	end    
})

MainTab:AddButton({
	Name = "AirSwim",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/HeyGyt/airswim/main/main"))()
  	end    
})





--GamesTab
local Games = Window:MakeTab({
	Name = "GamesðŸŽ®",
	Icon = nil,
	PremiumOnly = false
})


Games:AddButton({
	Name = "ðŸ BrookhavenðŸ ",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/IceMael7/NewIceHub/main/Brookhaven"))()
  	end    
})


Games:AddButton({
	Name = "ðŸ”ªMM2ðŸ”ª",
	Callback = function()
      	loadstring(game:HttpGet(('https://raw.githubusercontent.com/MarsQQ/ScriptHubScripts/master/MM2%20Admin%20Panel'),true))()
  	end    
})

Games:AddButton({
	Name = "Flee The Facility",
	Callback = function()
      	loadstring(game:HttpGet("https://raw.githubusercontent.com/LeviTheOtaku/roblox-scripts/main/FTFHAX.lua%22,true))()	
  	end    
})

Games:AddButton({
	Name = "BedwarsðŸ›Œ",
	Callback = function()
      	loadstring(game:HttpGet("https://raw.githubusercontent.com/7GrandDadPGN/VapeV4ForRoblox/main/NewMainScript.lua", true))()	
  	end    
})

Games:AddButton({
	Name = "ðŸ”«Big PaintballðŸ”«",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/AndrewDarkyy/NOWAY/main/darkyyware.lua%22))()
  	end    
})

Games:AddButton({
	Name = "Combat Warriors",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/SussyImposterRed/Scripts/main/NEW_NOVA"))()
  	end    
})

Games:AddButton({
	Name = "Blox Fruits",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/Domadicoof/Domadicoof/main/Domadichub/NottoGay/Start.ranscript%22))()
  	end    
})

Games:AddButton({
	Name = "Prison Life",
	Callback = function()
      		loadstring(game:HttpGet('https://pastebin.com/raw/iZ64yzjE'))()
  	end    
})

Games:AddButton({
	Name = "âš¡Legends of Speedâš¡",
	Callback = function()
      		loadstring(game:HttpGet("https://pastebin.com/raw/1iMHrZ50", true))()
  	end    
})

Games:AddButton({
	Name = "ðŸ’ªMuscle LegendsðŸ’ª",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/harisiskandar178/Roblox-Script/main/Muscle%20Legend"))()
  	end    
})

Games:AddButton({
	Name = "Break In",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/TrixAde/Proxima-Hub/main/Main.lua"))()
  	end    
})

Games:AddButton({
	Name = "Nico's Nextbots",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/GamingScripter/Darkrai-X/main/Games/NicoNextBots", true))()
  	end    
})

Games:AddButton({
	Name = "DoorsðŸ‘",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/GamingScripter/Darkrai-X/main/Games/Doors"))()
  	end    
})

Games:AddButton({
	Name = "Evade",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/GamingScripter/Darkrai-X/main/Games/Evade"))()
  	end    
})

Games:AddButton({
	Name = "Rainbow Friends",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/JNHHGaming/Rainbow-Friends/main/Rainbow%20Friends"))()
  	end    
})

Games:AddButton({
	Name = "Slap Battles",
	Callback = function()
      		loadstring(game:HttpGet(('https://raw.githubusercontent.com/TheScriptMaster1/ScriptMaster-Hub/main/scriptmasterhub.lua')))()
  	end    
})

Games:AddButton({
	Name = "Pop it trading",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/scripthubekitten/SCRIPTHUBV2/main/SCRIPTHUBV2", true))()
  	end    
})

Games:AddButton({
	Name = "JailBreak",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/scripthubekitten/SCRIPTHUBV2/main/SCRIPTHUBV2", true))()
  	end    
})



--Admins
local Admins = Window:MakeTab({
	Name = "Admins",
	Icon = nil,
	PremiumOnly = false
})

Admins:AddButton({
	Name = "Infinite Yield",
	Callback = function()
      		loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
  	end    
})

Admins:AddButton({
	Name = "CMD-X",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/CMD-X/CMD-X/master/Source", true))()
  	end    
})





Admins:AddButton({
	Name = "Fates Admin",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/fatesc/fates-admin/main/main.lua"))()
  	end    
})



--Misc
local Misc = Window:MakeTab({
	Name = "Misc",
	Icon = nil,
	PremiumOnly = false
})

Misc:AddButton({
	Name = "Keyboard",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/advxzivhsjjdhxhsidifvsh/mobkeyboard/main/main.txt", true))()
  	end    
})

Misc:AddButton({
	Name = "FE Animations GUI",
	Callback = function()
      		loadstring(game:HttpGet("https://raw.githubusercontent.com/GamingScripter/Animation-Hub/main/Animation%20Gui", true))()
  	end    
})

Misc:AddButton({
	Name = "Free Emotes",
	Callback = function()
	        loadstring(game:HttpGet("https://pastebin.com/raw/eCpipCTH%22))()
  	end    
})

Misc:AddButton({
	Name = "Rejoin",
	Callback = function()
      		local ts = game:GetService("TeleportService")

local p = game:GetService("Players").LocalPlayer

 

ts:Teleport(game.PlaceId, p)
  	end    
})

Misc:AddButton({
	Name = "",
	Callback = function()
      		
  	end    
})





--Credits
local Credits = Window:MakeTab({
	Name = "Credits",
	Icon = nil,
	PremiumOnly = false
})



Credits:AddLabel("Made by Deadly_Frenzy_")
Credits:AddLabel("Sub to Deadly_Frenzy_ on YouTube")
Credits:AddLabel("Follow deadly_frenzy_ on TikTok")
Credits:AddLabel("Deadly_Frenzy_ Roblox Account: F0X42512")
Credits:AddLabel("")
Credits:AddLabel("imgood_atnameing_things helped me")
Credits:AddLabel("Follow imgood_atnameing_things on TikTok")
Credits:AddLabel("imgood_atnameing_things Roblox Account: duckarmy609")






end
OrionLib:Init()
