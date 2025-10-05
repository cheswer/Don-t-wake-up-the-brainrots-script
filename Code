local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local player = Players.LocalPlayer

-- Asegurar que PlayerGui esté cargado
local playerGui = player:WaitForChild("PlayerGui")

-- Crear ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "DWUTB_Hub"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Crear Frame
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 200, 0, 220)
frame.Position = UDim2.new(0, 20, 0.5, -110)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.BorderSizePixel = 0
frame.Parent = screenGui

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 30)
title.Text = "DWUTB Hub"
title.TextColor3 = Color3.new(1, 1, 1)
title.BackgroundTransparency = 1
title.Font = Enum.Font.SourceSansBold
title.TextSize = 20
title.Parent = frame

-- Variables
local savedPosition = nil
local noclipEnabled = false
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- Botón genérico
local function createButton(name, text, posY, onClick)
	local button = Instance.new("TextButton")
	button.Name = name
	button.Size = UDim2.new(1, -20, 0, 40)
	button.Position = UDim2.new(0, 10, 0, posY)
	button.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
	button.TextColor3 = Color3.new(1, 1, 1)
	button.Font = Enum.Font.SourceSans
	button.TextSize = 16
	button.Text = text
	button.Parent = frame

	button.MouseButton1Click:Connect(onClick)
end

-- GUARDARPOSICIÓN
createButton("GuardarPos", "GUARDARPOSICIÓN", 40, function()
	character = player.Character or player.CharacterAdded:Wait()
	humanoidRootPart = character:WaitForChild("HumanoidRootPart")
	savedPosition = humanoidRootPart.Position
	print("[DWUTB] Posición guardada:", savedPosition)
end)

-- InstaSteal
createButton("InstaSteal", "InstaSteal", 90, function()
	if savedPosition then
		character = player.Character or player.CharacterAdded:Wait()
		humanoidRootPart = character:WaitForChild("HumanoidRootPart")
		humanoidRootPart.CFrame = CFrame.new(savedPosition)
		print("[DWUTB] Teletransportado.")
	else
		warn("[DWUTB] No hay posición guardada.")
	end
end)

-- BoostVelocidad
createButton("BoostVelocidad", "BoostVelocidad", 140, function()
	local humanoid = character:FindFirstChildWhichIsA("Humanoid")
	if humanoid then
		humanoid.WalkSpeed = 45
		print("[DWUTB] Velocidad aumentada.")
	end
end)

-- Noclip
createButton("Noclip", "Noclip (Toggle)", 190, function()
	noclipEnabled = not noclipEnabled
	print("[DWUTB] Noclip " .. (noclipEnabled and "Activado" or "Desactivado"))
end)

-- Loop de Noclip
RunService.Stepped:Connect(function()
	if noclipEnabled then
		for _, part in pairs(player.Character:GetDescendants()) do
			if part:IsA("BasePart") then
				part.CanCollide = false
			end
		end
	end
end)

-- Actualizar character si respawnea
player.CharacterAdded:Connect(function(char)
	character = char
	humanoidRootPart = char:WaitForChild("HumanoidRootPart")
end)
