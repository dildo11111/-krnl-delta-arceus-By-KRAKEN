-- Сделано Darklless'om и Kraken
local player = game.Players.LocalPlayer
local gui = player.PlayerGui

local function createNotification(message)
    local notification = Instance.new("ScreenGui")
    notification.Name = "Notification"
    notification.Parent = gui

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 200, 0, 50)
    frame.Position = UDim2.new(0.5, -100, 0, 10)
    frame.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
    frame.BorderSizePixel = 2
    frame.Parent = notification

    local textLabel = Instance.new("TextLabel")
    textLabel.Text = message
    textLabel.Size = UDim2.new(1, 0, 1, 0)
    textLabel.TextScaled = true
    textLabel.Parent = frame

    wait(1)
    notification:Destroy()
end

local speedWalkGui = Instance.new("ScreenGui")
speedWalkGui.Parent = gui
speedWalkGui.IgnoreGuiInset = true  
speedWalkGui.Enabled = true

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 200, 0, 140)
frame.Position = UDim2.new(0.5, -100, 0, 10)
frame.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
frame.BorderSizePixel = 2
frame.Parent = speedWalkGui

local walkSpeedTextBox = Instance.new("TextBox")
walkSpeedTextBox.Position = UDim2.new(0, 10, 0, 10)
walkSpeedTextBox.Size = UDim2.new(0, 80, 0, 20)
walkSpeedTextBox.Parent = frame

local jumpPowerTextBox = Instance.new("TextBox")
jumpPowerTextBox.Position = UDim2.new(0, 120, 0, 10)
jumpPowerTextBox.Size = UDim2.new(0, 80, 0, 20)
jumpPowerTextBox.Parent = frame

local applyButton = Instance.new("TextButton")
applyButton.Text = "Сохранить дилдо"
applyButton.Position = UDim2.new(0.5, -80, 0, 40)
applyButton.Size = UDim2.new(0, 160, 0, 20)
applyButton.Parent = frame

local resetButton = Instance.new("TextButton")
resetButton.Text = "Ресетнуть"
resetButton.Position = UDim2.new(0.5, -80, 0, 70)
resetButton.Size = UDim2.new(0, 160, 0, 20)
resetButton.Parent = frame

local toggleButton = Instance.new("TextButton")
toggleButton.Text = "Закрыть пизду"
toggleButton.Position = UDim2.new(0.5, -80, 0, 110)
toggleButton.Size = UDim2.new(0, 160, 0, 20)
toggleButton.Parent = frame

applyButton.MouseButton1Click:Connect(function()
    local walkSpeed = tonumber(walkSpeedTextBox.Text) or 16
    local jumpPower = tonumber(jumpPowerTextBox.Text) or 50

    local character = player.Character
    if character and character:FindFirstChildOfClass("Humanoid") then
        character:FindFirstChildOfClass("Humanoid").WalkSpeed = walkSpeed
        character:FindFirstChildOfClass("Humanoid").JumpPower = jumpPower
    end

    createNotification("Сохранено!")
end)

resetButton.MouseButton1Click:Connect(function()
    walkSpeedTextBox.Text = ""
    jumpPowerTextBox.Text = ""

    local character = player.Character
    if character and character:FindFirstChildOfClass("Humanoid") then
        character:FindFirstChildOfClass("Humanoid").WalkSpeed = 16
        character:FindFirstChildOfClass("Humanoid").JumpPower = 50
    end

    createNotification("Дилдаки ресетнулись")
end)

-- Function to handle toggle button click
toggleButton.MouseButton1Click:Connect(function()
    speedWalkGui.Enabled = not speedWalkGui.Enabled
end)
