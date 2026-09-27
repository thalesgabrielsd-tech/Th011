local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local player = Players.LocalPlayer

local openEgg = ReplicatedStorage:WaitForChild("OpenEgg")
local selectEgg = ReplicatedStorage:WaitForChild("SelectEgg")

local gui = Instance.new("ScreenGui")
gui.Name = "EggGUI"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(0, 400, 0, 50)
title.Position = UDim2.new(0.5, -200, 0, 30)
title.Text = "🥚 SISTEMA DE OVOS"
title.TextScaled = true
title.Parent = gui

-- Resultado
local result = Instance.new("TextLabel")
result.Size = UDim2.new(0, 500, 0, 70)
result.Position = UDim2.new(0.5, -250, 0, 90)
result.Text = "Selecione um ovo!"
result.TextScaled = true
result.Parent = gui

local eggs = {
	"Ovo Divino",
	"Ovo Eterno",
	"Ovo Cósmico",
	"Ovo Secreto"
}

local y = 180

for _, eggName in ipairs(eggs) do

	local button = Instance.new("TextButton")

	button.Size = UDim2.new(0, 300, 0, 50)
	button.Position = UDim2.new(0.5, -150, 0, y)

	button.Text = eggName
	button.TextScaled = true
	button.Parent = gui

	button.MouseButton1Click:Connect(function()

		selectEgg:FireServer(eggName)

		result.Text = "Selecionado: " .. eggName

	end)

	y += 60

end

-- Botão abrir
local openButton = Instance.new("TextButton")

openButton.Size = UDim2.new(0, 300, 0, 60)
openButton.Position = UDim2.new(0.5, -150, 0, y + 20)

openButton.Text = "🥚 ABRIR OVO"
openButton.TextScaled = true
openButton.Parent = gui

openButton.MouseButton1Click:Connect(function()
	openEgg:FireServer()
end)

-- Recebe resultado
openEgg.OnClientEvent:Connect(function(eggName, rarity)

	result.Text =
		eggName ..
		" → ✨ " ..
		rarity

end)
