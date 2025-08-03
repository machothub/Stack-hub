-- Stack Hub | Mod Menu para Steal a Brainrot
-- Interface parecida com a do "MIRANDA VIP+"
-- Script 100% open source

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")

-- Interface
local ScreenGui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
ScreenGui.Name = "StackHubUI"

local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 220, 0, 180)
Frame.Position = UDim2.new(0.05, 0, 0.2, 0)
Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Frame.BorderSizePixel = 2
Frame.BorderColor3 = Color3.fromRGB(255, 0, 0)

local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1, 0, 0, 25)
Title.Text = "STACK HUB VIP+"
Title.BackgroundTransparency = 1
Title.TextColor3 = Color3.fromRGB(255, 0, 0)
Title.Font = Enum.Font.Code
Title.TextSize = 18

local function createButton(name, position, callback)
    local btn = Instance.new("TextButton", Frame)
    btn.Size = UDim2.new(1, -10, 0, 30)
    btn.Position = UDim2.new(0, 5, 0, position)
    btn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    btn.TextColor3 = Color3.fromRGB(255, 0, 0)
    btn.Font = Enum.Font.Code
    btn.Text = name
    btn.TextSize = 16
    btn.MouseButton1Click:Connect(callback)
    return btn
end

-- Funções do Menu

-- 🦘 Super Jump
createButton("Super Jump", 30, function()
    local humanoid = Character:FindFirstChildOfClass("Humanoid")
    if humanoid then
        humanoid.UseJumpPower = true
        humanoid.JumpPower = 200
    end
end)

-- 🧲 Flutuar até a base
createButton("Flutuar até a Base", 70, function()
    local basePos = workspace:FindFirstChild("Base") -- ajuste se necessário
    if basePos then
        local connection
        connection = RunService.RenderStepped:Connect(function()
            HumanoidRootPart.CFrame = HumanoidRootPart.CFrame:Lerp(basePos.CFrame + Vector3.new(0, 30, 0), 0.1)
        end)
        wait(5)
        if connection then connection:Disconnect() end
    end
end)

-- 🕒 Mostrar tempo da base
createButton("Tempo da Base", 110, function()
    local timer = workspace:FindFirstChild("BaseTimer") -- ajuste se necessário
    if timer and timer:IsA("TextLabel") then
        print("Tempo restante da base:", timer.Text)
    else
        warn("Timer da base não encontrado!")
    end
end)

-- 🧠 Mostrar Brainrot God/Secrete
createButton("Ver Brainrot God/Secrete", 150, function()
    for _, obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("Model") and (obj.Name:lower():find("god") or obj.Name:lower():find("secrete")) then
            local highlight = Instance.new("Highlight", obj)
            highlight.FillColor = Color3.fromRGB(255, 215, 0)
            highlight.OutlineColor = Color3.fromRGB(255, 0, 0)
        end
    end
end)

-- Interface draggable
Frame.Active = true
Frame.Draggable = true
