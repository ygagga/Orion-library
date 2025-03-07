local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

-- Criando a janela principal da interface
local Window = OrionLib:MakeWindow({
    Name = "Troll Hub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TrollHubConfig"
})

-----------------------------------------------------------
-- Criando as Abas
-----------------------------------------------------------

-- 👾 Troll
local TrollTab = Window:MakeTab({
    Name = "Trolls",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- 🎶 Música
local MusicTab = Window:MakeTab({
    Name = "Música",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- ⚡ Hacks
local HacksTab = Window:MakeTab({
    Name = "Hacks",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- 🧑‍💻 Scripts
local ScriptsTab = Window:MakeTab({
    Name = "Scripts",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- ℹ️ Sobre
local AboutTab = Window:MakeTab({
    Name = "Sobre",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-----------------------------------------------------------
-- Funções de Troll
-----------------------------------------------------------

TrollTab:AddSection("Controle de Jogadores")

TrollTab:AddInput("PlayerName", {
    Title = "Nome do Jogador",
    Default = "",
    Placeholder = "Digite o nome do jogador",
    Callback = function(value)
        selectedPlayer = value
    end
})

TrollTab:AddButton({
    Title = "Teleportar Todos 🏃‍♂️",
    Description = "Teleporta todos os jogadores para você!",
    Callback = function()
        teleportAllPlayers()
    end
})

TrollTab:AddButton({
    Title = "Espectar 👀",
    Description = "Veja o que o jogador está fazendo",
    Callback = function()
        if selectedPlayer ~= "" then
            spectatePlayer(selectedPlayer)
        end
    end
})

TrollTab:AddButton({
    Title = "Despectar 🚶‍♂️",
    Description = "Volte para o seu personagem!",
    Callback = function()
        if isSpectating then
            despectatePlayer()
        end
    end
})

-----------------------------------------------------------
-- Funções de Música
-----------------------------------------------------------

MusicTab:AddSection("Reproduzir Música para Todos")

MusicTab:AddInput("MusicID", {
    Title = "ID da Música",
    Default = "",
    Placeholder = "Digite o ID da música",
    Numeric = true,
    Finished = true,
    Callback = function(value)
        musicId = value
    end
})

MusicTab:AddToggle("LoopMusic", {
    Title = "Loop",
    Default = false,
    Callback = function(value)
        loopMusic = value
    end
})

MusicTab:AddButton({
    Title = "Reproduzir Música 🎶",
    Description = "Reproduza a música para todos os jogadores.",
    Callback = function()
        if musicId ~= "" then
            playMusicForAll(musicId, loopMusic)
        end
    end
})

-----------------------------------------------------------
-- Funções de Hacks
-----------------------------------------------------------

HacksTab:AddSection("Superpoderes!")

HacksTab:AddButton({
    Title = "Ativar Super Velocidade ⚡",
    Description = "Corre mais rápido que o Flash!",
    Callback = function()
        toggleSpeed(true)
    end
})

HacksTab:AddButton({
    Title = "Desativar Velocidade ❌",
    Description = "Desativa a Super Velocidade!",
    Callback = function()
        toggleSpeed(false)
    end
})

HacksTab:AddButton({
    Title = "Ativar Pulo Infinito 🦘",
    Description = "Pule o quanto quiser sem limites!",
    Callback = function()
        toggleJump(true)
    end
})

HacksTab:AddButton({
    Title = "Desativar Pulo Infinito ❌",
    Description = "Desativa o Pulo Infinito!",
    Callback = function()
        toggleJump(false)
    end
})

HacksTab:AddButton({
    Title = "Ativar Atravessar Paredes 🚪",
    Description = "Agora você pode atravessar as paredes!",
    Callback = function()
        toggleWallWalk(true)
    end
})

HacksTab:AddButton({
    Title = "Desativar Atravessar Paredes ❌",
    Description = "Desativa o poder de atravessar paredes!",
    Callback = function()
        toggleWallWalk(false)
    end
})

-----------------------------------------------------------
-- Scripts
-----------------------------------------------------------

ScriptsTab:AddSection("Carregar Scripts")

ScriptsTab:AddButton({
    Title = "Fly Script ✈️",
    Description = "Ativa o Fly script.",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()
    end
})

ScriptsTab:AddButton({
    Title = "RAEL Hub 🔧",
    Description = "Carrega o RAEL Hub.",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Laelmano24/Rael-Hub/main/main.txt"))()
    end
})

ScriptsTab:AddButton({
    Title = "Sander X 🛸",
    Description = "Carrega o Sander X.",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/sXPiterXs1111/Sanderxv3.30/main/sanderx3.30'))()
    end
})

-----------------------------------------------------------
-- Sobre
-----------------------------------------------------------

AboutTab:AddSection("Informações do Criador")

AboutTab:AddParagraph("Criado por Shelby, Discord: snobodj")
AboutTab:AddParagraph("Criado para bagunçar no Brookhaven RP! Aproveite e divirta-se, mas sem exagerar! 😆")

-----------------------------------------------------------
-- Finalizando a interface
-----------------------------------------------------------

OrionLib:Init()
