-- VictorLouHub Neon Supremo - Com Fly, Teleport, NoClip, WalkSpeed, JumpPower, Som, Salvamento e botão abrir arrastável

-- Referência ao jogador
local player = game.Players.LocalPlayer
repeat wait() until player.Character and player.Character:FindFirstChild("Humanoid")
local character = player.Character

-- Serviços
local RunService = game:GetService("RunService")
local TeleportService = game:GetService("TeleportService")
local HttpService = game:GetService("HttpService")

-- Sons
local function playSound(id)
    local s = Instance.new("Sound")
    s.SoundId = "rbxassetid://" .. id
    s.Volume = 1
    s.PlayOnRemove = true
    s.Parent = workspace
    s:Destroy()
end

-- Salvamento
local settingsFile = "VictorLou_Settings.json"
local saved = {}

pcall(function()
    local data = readfile and readfile(settingsFile)
    if data then saved = HttpService:JSONDecode(data) end
end)

local function saveSettings()
    if writefile then
        writefile(settingsFile, HttpService:JSONEncode(saved))
    end
end

-- GUI
local gui = Instance.new("ScreenGui", game.CoreGui)
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 360, 0, 370)
frame.Position = UDim2.new(0.3, 0, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
frame.BorderColor3 = Color3.fromRGB(0, 255, 255)
frame.BorderSizePixel = 3
frame.Active = true
frame.Draggable = true

local function neonStroke(obj, color)
    local stroke = Instance.new("UIStroke", obj)
    stroke.Color = color
    stroke.Thickness = 3
    stroke.Transparency = 0
end

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0, 40)
title.Text = "💎 VictorLouHub - NEON"
title.Font = Enum.Font.GothamBlack
title.TextSize = 20
title.TextColor3 = Color3.fromRGB(0, 255, 255)
title.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
neonStroke(title, Color3.fromRGB(0,255,255))

-- TextBoxes
local function createBox(placeholder, yPos)
    local box = Instance.new("TextBox", frame)
    box.Size = UDim2.new(0.85, 0, 0, 30)
    box.Position = UDim2.new(0.075, 0, yPos, 0)
    box.PlaceholderText = placeholder
    box.Text = ""
    box.Font = Enum.Font.Gotham
    box.TextSize = 16
    box.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    box.TextColor3 = Color3.fromRGB(0,255,0)
    neonStroke(box, Color3.fromRGB(0,255,0))
    return box
end

local speedBox = createBox("WalkSpeed", 0.15)
local jumpBox = createBox("JumpPower", 0.27)

-- Botões
local function createButton(text, yPos, color)
    local btn = Instance.new("TextButton", frame)
    btn.Size = UDim2.new(0.85, 0, 0, 30)
    btn.Position = UDim2.new(0.075, 0, yPos, 0)
    btn.Text = text
    btn.Font = Enum.Font.GothamBlack
    btn.TextSize = 16
    btn.BackgroundColor3 = color
    btn.TextColor3 = Color3.new(1,1,1)
    neonStroke(btn, color)
    return btn
end

local applyBtn = createButton("✅ Aplicar", 0.4, Color3.fromRGB(0, 200, 0))
local noclipBtn = createButton("🚫 NoClip: OFF", 0.52, Color3.fromRGB(0, 0, 200))
local flyBtn = createButton("🕊️ Fly: OFF", 0.64, Color3.fromRGB(255, 100, 0))
local tpBtn = createButton("🌀 Teleport para Frente", 0.76, Color3.fromRGB(100, 0, 200))

local closeBtn = Instance.new("TextButton", frame)
closeBtn.Text = "😺"
closeBtn.Size = UDim2.new(0, 40, 0, 40)
closeBtn.Position = UDim2.new(1, -40, 0, 0)
closeBtn.BackgroundColor3 = Color3.fromRGB(255, 80, 80)
closeBtn.TextColor3 = Color3.new(1,1,1)
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 22

local openBtn = Instance.new("TextButton", gui)
openBtn.Text = "💀"
openBtn.Size = UDim2.new(0, 50, 0, 50)
openBtn.Position = UDim2.new(0, 10, 0.5, 0)
openBtn.BackgroundColor3 = Color3.fromRGB(10,10,10)
openBtn.TextColor3 = Color3.fromRGB(0,255,255)
openBtn.Font = Enum.Font.GothamBlack
openBtn.TextSize = 30
openBtn.Visible = false

-- Função para tornar GUI arrastável (drag)
local function makeDraggable(guiObject)
    local dragging = false
    local dragInput, dragStart, startPos

    guiObject.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            dragStart = input.Position
            startPos = guiObject.Position

            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    guiObject.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement then
            dragInput = input
        end
    end)

    RunService.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            local delta = input.Position - dragStart
            local newX = math.clamp(startPos.X.Offset + delta.X, 0, workspace.CurrentCamera.ViewportSize.X - guiObject.AbsoluteSize.X)
            local newY = math.clamp(startPos.Y.Offset + delta.Y, 0, workspace.CurrentCamera.ViewportSize.Y - guiObject.AbsoluteSize.Y)
            guiObject.Position = UDim2.new(0, newX, 0, newY)
        end
    end)
end

-- Aplica drag no botão de abrir
makeDraggable(openBtn)

-- Lógica dos botões
applyBtn.MouseButton1Click:Connect(function()
    local hum = character:FindFirstChild("Humanoid")
    if hum then
        local ws = tonumber(speedBox.Text)
        local jp = tonumber(jumpBox.Text)
        if ws then hum.WalkSpeed = ws saved.ws = ws end
        if jp then hum.JumpPower = jp saved.jp = jp end
        saveSettings()
        playSound("12222030")
    end
end)

local noclip = false
local fly = false
local flyVel, flyGyro, flyConn

noclipBtn.MouseButton1Click:Connect(function()
    noclip = not noclip
    noclipBtn.Text = "🚫 NoClip: " .. (noclip and "ON" or "OFF")
    if noclip then
        flyConn = RunService.Stepped:Connect(function()
            for _, p in pairs(character:GetDescendants()) do
                if p:IsA("BasePart") then p.CanCollide = false end
            end
        end)
    elseif flyConn then flyConn:Disconnect() end
    playSound("12222030")
end)

flyBtn.MouseButton1Click:Connect(function()
    fly = not fly
    flyBtn.Text = "🕊️ Fly: " .. (fly and "ON" or "OFF")
    if fly then
        flyGyro = Instance.new("BodyGyro", character.HumanoidRootPart)
        flyGyro.MaxTorque = Vector3.new(400000,400000,400000)
        flyGyro.P = 10000
        flyVel = Instance.new("BodyVelocity", character.HumanoidRootPart)
        flyVel.MaxForce = Vector3.new(100000,100000,100000)
        flyVel.Velocity = Vector3.zero

        flyConn = RunService.RenderStepped:Connect(function()
            flyGyro.CFrame = workspace.CurrentCamera.CFrame
            flyVel.Velocity = workspace.CurrentCamera.CFrame.LookVector * 100
        end)
    else
        flyConn:Disconnect()
        flyGyro:Destroy()
        flyVel:Destroy()
    end
    playSound("12222030")
end)

tpBtn.MouseButton1Click:Connect(function()
    character:MoveTo(character.HumanoidRootPart.Position + workspace.CurrentCamera.CFrame.LookVector * 30)
    playSound("9118823098")
end)

closeBtn.MouseButton1Click:Connect(function()
    frame.Visible = false
    openBtn.Visible = true
    playSound("9118823101")
end)

openBtn.MouseButton1Click:Connect(function()
    frame.Visible = true
    openBtn.Visible = false
    playSound("9118823098")
end)

-- Carrega configurações salvas
if saved.ws then character.Humanoid.WalkSpeed = saved.ws speedBox.Text = tostring(saved.ws) end
if saved.jp then character.Humanoid.JumpPower = saved.jp jumpBox.Text = tostring(saved.jp) end
