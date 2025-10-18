-- The King Mod V1 - COMPLETO E COMPATÍVEL

-- Serviços
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera

-- Variáveis
local headshotEnabled = false
local walkspeedEnabled = false
local fovEnabled = false
local fovSize = 150
local walkSpeedValue = 16

-- GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TheKingModV1"
screenGui.Parent = LocalPlayer:WaitForChild("PlayerGui") -- Compatível com todos executores

-- --- TELA DE LOGIN ---
local loginFrame = Instance.new("Frame")
loginFrame.Size = UDim2.new(0,300,0,150)
loginFrame.Position = UDim2.new(0.5,-150,0.5,-75)
loginFrame.BackgroundColor3 = Color3.fromRGB(20,20,20)
loginFrame.BorderSizePixel = 0
loginFrame.Parent = screenGui

local loginText = Instance.new("TextLabel")
loginText.Size = UDim2.new(1,0,0,50)
loginText.Position = UDim2.new(0,0,0,0)
loginText.Text = "The King Mod V1"
loginText.TextColor3 = Color3.fromRGB(255,255,255)
loginText.BackgroundTransparency = 1
loginText.Font = Enum.Font.SourceSansBold
loginText.TextScaled = true
loginText.Parent = loginFrame

local passwordBox = Instance.new("TextBox")
passwordBox.Size = UDim2.new(0.8,0,0,40)
passwordBox.Position = UDim2.new(0.1,0,0.4,0)
passwordBox.PlaceholderText = "Digite a senha"
passwordBox.Text = ""
passwordBox.ClearTextOnFocus = true
passwordBox.BackgroundColor3 = Color3.fromRGB(35,35,35)
passwordBox.TextColor3 = Color3.fromRGB(255,255,255)
passwordBox.Parent = loginFrame

local loginButton = Instance.new("TextButton")
loginButton.Size = UDim2.new(0.6,0,0,30)
loginButton.Position = UDim2.new(0.2,0,0.7,0)
loginButton.Text = "Entrar"
loginButton.BackgroundColor3 = Color3.fromRGB(50,50,50)
loginButton.TextColor3 = Color3.fromRGB(255,255,255)
loginButton.Parent = loginFrame

-- --- HUB ---
local hubFrame = Instance.new("Frame")
hubFrame.Size = UDim2.new(0,400,0,300)
hubFrame.Position = UDim2.new(0.5,-200,0.5,-150)
hubFrame.BackgroundColor3 = Color3.fromRGB(20,20,20)
hubFrame.Visible = false
hubFrame.Parent = screenGui

local hubTitle = Instance.new("TextLabel")
hubTitle.Size = UDim2.new(1,0,0,40)
hubTitle.Position = UDim2.new(0,0,0,0)
hubTitle.Text = "The King Mod V1"
hubTitle.TextColor3 = Color3.fromRGB(255,255,255)
hubTitle.BackgroundTransparency = 1
hubTitle.Font = Enum.Font.SourceSansBold
hubTitle.TextScaled = true
hubTitle.Parent = hubFrame

-- Botão minimizar
local minimizeBtn = Instance.new("TextButton")
minimizeBtn.Size = UDim2.new(0,30,0,30)
minimizeBtn.Position = UDim2.new(1,-35,0,5)
minimizeBtn.Text = "-"
minimizeBtn.TextColor3 = Color3.fromRGB(255,255,255)
minimizeBtn.BackgroundColor3 = Color3.fromRGB(50,50,50)
minimizeBtn.Parent = hubFrame

-- Botão reabrir
local reopenBtn = Instance.new("TextButton")
reopenBtn.Size = UDim2.new(0,50,0,50)
reopenBtn.Position = UDim2.new(0,10,0,10)
reopenBtn.Text = "MOD"
reopenBtn.TextColor3 = Color3.fromRGB(255,255,255)
reopenBtn.BackgroundColor3 = Color3.fromRGB(50,50,50)
reopenBtn.Visible = false
reopenBtn.Parent = screenGui
reopenBtn.TextScaled = true
reopenBtn.AutoButtonColor = true
reopenBtn.TextWrapped = true
reopenBtn.TextXAlignment = Enum.TextXAlignment.Center
reopenBtn.TextYAlignment = Enum.TextYAlignment.Center
reopenBtn.BorderSizePixel = 0

minimizeBtn.MouseButton1Click:Connect(function()
    hubFrame.Visible = false
    reopenBtn.Visible = true
end)
reopenBtn.MouseButton1Click:Connect(function()
    hubFrame.Visible = true
    reopenBtn.Visible = false
end)

-- --- HEADSHOT ---
local headshotBtn = Instance.new("TextButton")
headshotBtn.Size = UDim2.new(0,150,0,40)
headshotBtn.Position = UDim2.new(0,20,0,60)
headshotBtn.Text = "HEADSHOT: OFF"
headshotBtn.TextColor3 = Color3.fromRGB(255,255,255)
headshotBtn.BackgroundColor3 = Color3.fromRGB(50,50,50)
headshotBtn.Parent = hubFrame

headshotBtn.MouseButton1Click:Connect(function()
    headshotEnabled = not headshotEnabled
    headshotBtn.Text = "HEADSHOT: "..(headshotEnabled and "ON" or "OFF")
end)

-- --- FOV ---
local fovBtn = Instance.new("TextButton")
fovBtn.Size = UDim2.new(0,150,0,30)
fovBtn.Position = UDim2.new(0,20,0,110)
fovBtn.Text = "FOV: OFF"
fovBtn.TextColor3 = Color3.fromRGB(255,255,255)
fovBtn.BackgroundColor3 = Color3.fromRGB(50,50,50)
fovBtn.Parent = hubFrame

local fovBox = Instance.new("TextBox")
fovBox.Size = UDim2.new(0,100,0,30)
fovBox.Position = UDim2.new(0,180,0,110)
fovBox.PlaceholderText = "150"
fovBox.TextColor3 = Color3.fromRGB(255,255,255)
fovBox.BackgroundColor3 = Color3.fromRGB(35,35,35)
fovBox.Parent = hubFrame

fovBtn.MouseButton1Click:Connect(function()
    fovEnabled = not fovEnabled
    fovFrame.Visible = fovEnabled
end)

fovBox.FocusLost:Connect(function()
    local value = tonumber(fovBox.Text)
    if value then 
        fovSize = value
        fovFrame.Size = UDim2.new(0, fovSize*2, 0, fovSize*2)
    end
end)

-- --- WALKSPEED ---
local wsBtn = Instance.new("TextButton")
wsBtn.Size = UDim2.new(0,150,0,30)
wsBtn.Position = UDim2.new(0,20,0,160)
wsBtn.Text = "WALKSPEED: OFF"
wsBtn.TextColor3 = Color3.fromRGB(255,255,255)
wsBtn.BackgroundColor3 = Color3.fromRGB(50,50,50)
wsBtn.Parent = hubFrame

local wsBox = Instance.new("TextBox")
wsBox.Size = UDim2.new(0,100,0,30)
wsBox.Position = UDim2.new(0,180,0,160)
wsBox.PlaceholderText = "16"
wsBox.TextColor3 = Color3.fromRGB(255,255,255)
wsBox.BackgroundColor3 = Color3.fromRGB(35,35,35)
wsBox.Parent = hubFrame

wsBtn.MouseButton1Click:Connect(function()
    walkspeedEnabled = not walkspeedEnabled
    wsBtn.Text = "WALKSPEED: "..(walkspeedEnabled and "ON" or "OFF")
end)

wsBox.FocusLost:Connect(function()
    local value = tonumber(wsBox.Text)
    if value then walkSpeedValue = value end
end)

-- --- LOGIN ---
loginButton.MouseButton1Click:Connect(function()
    if passwordBox.Text == "le" then
        loginFrame.Visible = false
        hubFrame.Visible = true
        fovFrame.Visible = fovEnabled
    else
        passwordBox.Text = ""
    end
end)

-- --- FOV FRAME ---
fovFrame = Instance.new("Frame")
fovFrame.Size = UDim2.new(0,fovSize*2,0,fovSize*2)
fovFrame.Position = UDim2.new(0.5,-fovSize,0.5,-fovSize)
fovFrame.BackgroundColor3 = Color3.fromRGB(0,255,0)
fovFrame.BackgroundTransparency = 0.8
fovFrame.BorderSizePixel = 2
fovFrame.Visible = fovEnabled
fovFrame.Parent = screenGui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(1,0)
corner.Parent = fovFrame

-- --- UPDATE LOOP ---
RunService.RenderStepped:Connect(function()
    -- Fixa FOV no centro
    fovFrame.Position = UDim2.new(0.5,-fovFrame.Size.X.Offset/2,0.5,-fovFrame.Size.Y.Offset/2)

    -- WalkSpeed
    if walkspeedEnabled and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
        LocalPlayer.Character.Humanoid.WalkSpeed = walkSpeedValue
    end

    -- Headshot dentro do FOV
    if headshotEnabled then
        local closest
        local minDist = fovSize
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("Head") then
                local screenPos, onScreen = Camera:WorldToViewportPoint(player.Character.Head.Position)
                if onScreen then
                    local dist = (Vector2.new(screenPos.X,screenPos.Y) - Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2)).Magnitude
                    if dist < minDist then
                        minDist = dist
                        closest = player
                    end
                end
            end
        end
        if closest then
            local headPos = closest.Character.Head.Position
            -- Camera.CFrame protegido
            pcall(function()
                Camera.CFrame = CFrame.new(Camera.CFrame.Position, headPos)
            end)
        end
    end
end)# The-king-mod-v1
