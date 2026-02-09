-- CYBERNODRY ULTIMATE NEON HUB V3
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local Credits = Instance.new("TextLabel")
local ButtonsHolder = Instance.new("ScrollingFrame")
local UIGridLayout = Instance.new("UIGridLayout")
local CloseBtn = Instance.new("TextButton")
local MinimizeBtn = Instance.new("TextButton")

-- Configuração da GUI
ScreenGui.Name = "CyberElite_V3"
ScreenGui.Parent = game.CoreGui
ScreenGui.ResetOnSpawn = false

-- SOM DE CLICK (Hacker Style)
local ClickSound = Instance.new("Sound")
ClickSound.SoundId = "rbxassetid://5443380682" -- Som de click tech
ClickSound.Volume = 1
ClickSound.Parent = game.Workspace

-- FRAME PRINCIPAL (ESTILO DA FOTO DO ESQUELETO)
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(5, 15, 20)
MainFrame.BackgroundTransparency = 0.15
MainFrame.Position = UDim2.new(0.3, 0, 0.25, 0)
MainFrame.Size = UDim2.new(0, 580, 0, 420)
MainFrame.Active = true
MainFrame.Draggable = true

-- Borda Neon
local Stroke = Instance.new("UIStroke")
Stroke.Parent = MainFrame
Stroke.Color = Color3.fromRGB(0, 255, 255)
Stroke.Thickness = 3

local Corner = Instance.new("UICorner")
Corner.CornerRadius = UDim.new(0, 12)
Corner.Parent = MainFrame

-- TÍTULO
Title.Parent = MainFrame
Title.Size = UDim2.new(1, 0, 0, 50)
Title.Text = "「 CYBERNODRY ELITE 」"
Title.TextColor3 = Color3.fromRGB(0, 255, 255)
Title.BackgroundTransparency = 1
Title.Font = Enum.Font.Arcade
Title.TextSize = 26

-- CRÉDITOS
Credits.Parent = MainFrame
Credits.Position = UDim2.new(0, 20, 1, -30)
Credits.Size = UDim2.new(0, 200, 0, 20)
Credits.Text = "by: cybernodry"
Credits.TextColor3 = Color3.fromRGB(0, 255, 255)
Credits.BackgroundTransparency = 1
Credits.Font = Enum.Font.Code
Credits.TextSize = 16

-- BOTÕES DE CONTROLE
local function CreateControl(name, text, color, pos, action)
    local btn = Instance.new("TextButton")
    btn.Parent = MainFrame
    btn.Size = UDim2.new(0, 35, 0, 30)
    btn.Position = pos
    btn.Text = text
    btn.BackgroundColor3 = color
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Font = Enum.Font.GothamBold
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 6)
    btn.MouseButton1Click:Connect(function()
        ClickSound:Play()
        action()
    end)
end

CreateControl("X", "X", Color3.fromRGB(180, 0, 0), UDim2.new(1, -45, 0, 10), function() ScreenGui:Destroy() end)
CreateControl("-", "-", Color3.fromRGB(40, 40, 40), UDim2.new(1, -90, 0, 10), function()
    local isMin = MainFrame.Size.Y.Offset < 100
    MainFrame:TweenSize(isMin and UDim2.new(0, 580, 0, 420) or UDim2.new(0, 580, 0, 50), "Out", "Quart", 0.3, true)
    ButtonsHolder.Visible = isMin
end)

-- CONTAINER BOTÕES
ButtonsHolder.Parent = MainFrame
ButtonsHolder.Position = UDim2.new(0, 20, 0, 60)
ButtonsHolder.Size = UDim2.new(1, -40, 1, -100)
ButtonsHolder.BackgroundTransparency = 1
ButtonsHolder.ScrollBarThickness = 4

UIGridLayout.Parent = ButtonsHolder
UIGridLayout.CellPadding = UDim2.new(0, 12, 0, 12)
UIGridLayout.CellSize = UDim2.new(0, 128, 0, 45)

-- FUNÇÃO BOTÃO COM ILUMINAÇÃO MELHORADA
local function AddTechButton(Name, ScriptURL)
    local Btn = Instance.new("TextButton")
    local BStroke = Instance.new("UIStroke")
    local TStroke = Instance.new("UIStroke") -- Brilho na letra
    
    Btn.Parent = ButtonsHolder
    Btn.Text = Name:upper()
    Btn.BackgroundColor3 = Color3.fromRGB(10, 30, 40)
    Btn.TextColor3 = Color3.fromRGB(255, 255, 255) -- Letra Branca para ler melhor
    Btn.Font = Enum.Font.GothamBold
    Btn.TextSize = 12
    Btn.TextWrapped = true
    
    Instance.new("UICorner", Btn).CornerRadius = UDim.new(0, 5)
    
    BStroke.Parent = Btn
    BStroke.Color = Color3.fromRGB(0, 150, 255)
    BStroke.Thickness = 1.5

    -- Brilho na Letra (Isso faz a letra "saltar" da tela)
    TStroke.Parent = Btn
    TStroke.Thickness = 0.5
    TStroke.Color = Color3.fromRGB(0, 255, 255)
    TStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Contextual

    Btn.MouseEnter:Connect(function()
        Btn.BackgroundColor3 = Color3.fromRGB(0, 200, 255)
        Btn.TextColor3 = Color3.fromRGB(0, 0, 0) -- Inverte a cor pra destacar
        BStroke.Color = Color3.fromRGB(255, 255, 255)
    end)
    
    Btn.MouseLeave:Connect(function()
        Btn.BackgroundColor3 = Color3.fromRGB(10, 30, 40)
        Btn.TextColor3 = Color3.fromRGB(255, 255, 255)
        BStroke.Color = Color3.fromRGB(0, 150, 255)
    end)
    
    Btn.MouseButton1Click:Connect(function()
        ClickSound:Play()
        pcall(function() loadstring(game:HttpGet(ScriptURL))() end)
    end)
end

-- LISTA DE BOTÕES
local list = {
    {"RASTREADOR OBJ", "https://raw.githubusercontent.com/Davidfod/Rastreador_de_Objeto_script/refs/heads/main/CYBERNODRY.md"},
    {"RASTREADOR TOOL", "https://raw.githubusercontent.com/Davidfod/Rastreador_de_Tool/refs/heads/main/CYBERNODRY.md"},
    {"BLADE BALL", "https://raw.githubusercontent.com/Davidfod/SCRIPT-BLAD-BALL-BY-CYBERNODRY/refs/heads/main/CYBERNODRY.md"},
    {"PUXAR DADOS", "https://raw.githubusercontent.com/Davidfod/dados.script.bycybernodry/refs/heads/main/CYBER.md"},
    {"ME CRASH", "https://raw.githubusercontent.com/Davidfod/cybernodry/refs/heads/main/scriptcrash"},
    {"AUTO FARM PRES.", "https://raw.githubusercontent.com/Davidfod/autofarmpresentes/refs/heads/main/README.md"},
    {"EXECUTOR", "https://raw.githubusercontent.com/Davidfod/scriptexecutor/refs/heads/main/README.md"},
    {"FEEL THE SCRIPT", "https://raw.githubusercontent.com/Davidfod/scriptsexocyber/refs/heads/main/CYBERNODRY.md"},
    {"ROBLOX EGOR", "https://raw.githubusercontent.com/Davidfod/robloxegorscriptcyber/refs/heads/main/CYBERNODRY.md"},
    {"ANT AFK", "https://raw.githubusercontent.com/Davidfod/antafkscript/refs/heads/main/CYBERNODRY.md"},
    {"TP SCRIPT", "https://raw.githubusercontent.com/Davidfod/tpscript/refs/heads/main/CYBERNODRY.md"},
    {"FARM COMUNIDADE", "https://raw.githubusercontent.com/Davidfod/Comunidade.br.script_farm/refs/heads/main/CYBERNODRY.md"},
    {"SIMULADOR ANIMAL", "https://raw.githubusercontent.com/Davidfod/scriptSimuladoranimalvip/refs/heads/main/CYBERNODRY.md"},
    {"HITBOX", "https://raw.githubusercontent.com/Davidfod/hitboxscript/refs/heads/main/CYBERNODRY.md"},
    {"MIRA GRUDADA", "https://raw.githubusercontent.com/Davidfod/Mira_grudada_script/refs/heads/main/CYBERNODRY.md"},
    {"FPS BOOST", "https://raw.githubusercontent.com/Davidfod/melhorar_fps_script_bycybernodry/refs/heads/main/CYBERNODRY.md"},
    {"BIRD GAME", "https://raw.githubusercontent.com/Davidfod/bird_game_script_autofarm_bycybernodry_2.0/refs/heads/main/BYCYBERNODRY.md"},
    {"SWORD FIGHT", "https://raw.githubusercontent.com/Davidfod/Sword-Fight-for.ugc_script_bycybernodry/refs/heads/main/BYCYBERNODRY.md"},
    {"OBBY FREE UGC", "https://raw.githubusercontent.com/Davidfod/Obby-for-free-UGC_by_cybernodry/refs/heads/main/CYBERNODRY.md"},
    {"FLING TARGET", "https://raw.githubusercontent.com/Davidfod/Escolha-pessoa-fling/refs/heads/main/CYBERNODRY.md"},
    {"FLING (ND)", "https://raw.githubusercontent.com/Davidfod/Script-fling-criado-por-cybernodry/refs/heads/main/CYBERNODRY.md"},
    {"ANT FLING", "https://raw.githubusercontent.com/Davidfod/ant-fling-script-roblox-criado-por-cybernodry/refs/heads/main/BYCYBERNODRY.md"},
    {"LEGENDS OF SPEED", "https://raw.githubusercontent.com/Davidfod/Script-Legends-Of-Speed-autofarm/refs/heads/main/CYBERNODRY.md"},
    {"MAX RUN SIM", "https://raw.githubusercontent.com/Davidfod/Max-run-Simulatores-script/refs/heads/main/CYBERNODRY.md"},
    {"FLING ALL", "https://raw.githubusercontent.com/Davidfod/script-fling-all/refs/heads/main/CYBERNODRY.md"},
    {"NINJA LEGENDS", "https://raw.githubusercontent.com/Davidfod/Ninja-Lengends-Script-/refs/heads/main/CYBERNODRY.md"},
    {"FLING UPDATE", "https://raw.githubusercontent.com/Davidfod/script-fling-update-/refs/heads/main/CYBERNODRY.md"},
    {"TSUNAMI BIKE", "https://raw.githubusercontent.com/Davidfod/-CORRIDA-Escapa-do-Tsunami-de-Bicicleta-Script/refs/heads/main/CYBERNODRY.md"}
}

for _, v in pairs(list) do AddTechButton(v[1], v[2]) end
