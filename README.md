local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

-- Criando a janela principal da interface
local Window = OrionLib:MakeWindow({
    Name = "Brookhaven RP 🏡 (Troll Hub 🤡)",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "TrollHubConfig"
})

-- Criando as abas
local TrollTab = Window:MakeTab({
    Name = "🤡 Troll",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local MusicTab = Window:MakeTab({
    Name = "🎶 Música",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local HacksTab = Window:MakeTab({
    Name = "⚡ Hacks",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local ScriptsTab = Window:MakeTab({
    Name = "🧑‍💻 Scripts",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local AboutTab = Window:MakeTab({
    Name = "ℹ️ Sobre",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-----------------------------------------------------------
-- 🤡 Troll
-----------------------------------------------------------
local TrollSection = TrollTab:AddSection({
    Name = "Funções de Troll"
})

local selectedPlayer = ""
local isSpectating = false

TrollSection:AddInput({
    Name = "Nome do Jogador",
    Default = "",
    Placeholder = "Digite o nome do jogador",
    Callback = function(value)
        selectedPlayer = value
    end
})

TrollSection:AddButton({
    Name = "Matar Jogador",
    Callback = function()
        -- Função para matar o jogador
        print("Jogador Morto!")
        -- Exemplo de função para matar o jogador
        -- game:GetService("Players").LocalPlayer.Character:BreakJoints()
    end
})

TrollSection:AddButton({
    Name = "Teleportar Todos 🏃‍♂️",
    Description = "Teleporta todos os jogadores para você!",
    Callback = function()
        -- Função para teleportar todos os jogadores
        print("Todos Jogadores Teleportados!")
        -- Código para teleportar todos os jogadores
    end
})

TrollSection:AddButton({
    Name = "Espectar Jogador 👀",
    Description = "Veja o que o jogador está fazendo",
    Callback = function()
        if selectedPlayer ~= "" then
            -- Função para espectar o jogador
            print("Espectando jogador: " .. selectedPlayer)
            -- Espectar código (substitua pelo código real)
        end
    end
})

TrollSection:AddButton({
    Name = "Despectar 🚶‍♂️",
    Description = "Voltar para o seu personagem!",
    Callback = function()
        if isSpectating then
            -- Função para despectar (voltar para o personagem original)
            print("Despectando!")
            -- Código para despectar
        end
    end
})

-----------------------------------------------------------
-- 🎶 Música
-----------------------------------------------------------
local MusicSection = MusicTab:AddSection({
    Name = "Reproduzir Música para Todos"
})

local musicId = ""  -- ID da música a ser tocada
local loopMusic = false  -- Controle de loop da música

MusicSection:AddInput({
    Name = "ID da Música",
    Default = "",
    Placeholder = "Digite o ID da música",
    Numeric = true,
    Finished = true,
    Callback = function(value)
        musicId = value
    end
})

MusicSection:AddToggle({
    Name = "Loop",
    Default = false,
    Callback = function(value)
        loopMusic = value
    end
})

MusicSection:AddButton({
    Name = "Reproduzir Música 🎶",
    Description = "Reproduza a música para todos os jogadores.",
    Callback = function()
        if musicId ~= "" then
            -- Função para reproduzir música
            print("Reproduzindo Música ID: " .. musicId)
            -- Código para tocar música
        end
    end
})

-----------------------------------------------------------
-- ⚡ Hacks
-----------------------------------------------------------
local HacksSection = HacksTab:AddSection({
    Name = "Superpoderes!"
})

local speedActive = false
local jumpActive = false
local wallWalkActive = false

HacksSection:AddButton({
    Name = "Ativar Super Velocidade ⚡",
    Description = "Corre mais rápido que o Flash!",
    Callback = function()
        speedActive = true
        print("Super Velocidade Ativada!")
        -- Código para ativar super velocidade
    end
})

HacksSection:AddButton({
    Name = "Desativar Velocidade ❌",
    Description = "Desativa a Super Velocidade!",
    Callback = function()
        speedActive = false
        print("Super Velocidade Desativada!")
        -- Código para desativar super velocidade
    end
})

HacksSection:AddButton({
    Name = "Ativar Pulo Infinito 🦘",
    Description = "Pule o quanto quiser sem limites!",
    Callback = function()
        jumpActive = true
        print("Pulo Infinito Ativado!")
        -- Código para ativar pulo infinito
    end
})

HacksSection:AddButton({
    Name = "Desativar Pulo Infinito ❌",
    Description = "Desativa o Pulo Infinito!",
    Callback = function()
        jumpActive = false
        print("Pulo Infinito Desativado!")
        -- Código para desativar pulo infinito
    end
})

HacksSection:AddButton({
    Name = "Ativar Atravessar Paredes 🚪",
    Description = "Agora você pode atravessar as paredes!",
    Callback = function()
        wallWalkActive = true
        print("Atravessar Paredes Ativado!")
        -- Código para atravessar paredes
    end
})

HacksSection:AddButton({
    Name = "Desativar Atravessar Paredes ❌",
    Description = "Desativa o poder de atravessar paredes!",
    Callback = function()
        wallWalkActive = false
        print("Atravessar Paredes Desativado!")
        -- Código para desativar atravessar paredes
    end
})

-----------------------------------------------------------
-- 🧑‍💻 Scripts
-----------------------------------------------------------
local ScriptsSection = ScriptsTab:AddSection({
    Name = "Carregar Scripts"
})

ScriptsSection:AddButton({
    Name = "Fly Script ✈️",
    Description = "Ativa o Fly script.",
    Callback = function()
        print("Fly Script Ativado!")
        loadstring(game:HttpGet("https://raw.githubusercontent.com/mikeexc/Dsc-Mike-Fly-Gui/main/Fly%20Gui"))()
    end
})

ScriptsSection:AddButton({
    Name = "RAEL Hub 🔧",
    Description = "Carrega o RAEL Hub.",
    Callback = function()
        print("RAEL Hub Carregado!")
        -- Código para carregar o RAEL Hub
    end
})

ScriptsSection:AddButton({
    Name = "Sander X 🛸",
    Description = "Carrega o Sander X.",
    Callback = function()
        print("Sander X Carregado!")
        -- Código para carregar o Sander X
    end
})

-----------------------------------------------------------
-- ℹ️ Sobre
-----------------------------------------------------------
local AboutSection = AboutTab:AddSection({
    Name = "Sobre o Troll Hub"
})

AboutSection:AddParagraph("Criado por Shelby - Troll Hub para bagunçar no Brookhaven RP!")
AboutSection:AddParagraph("Aproveite e divirta-se, mas sem exagerar! 😆")

-- Finalizando a interface
OrionLib:Init()
