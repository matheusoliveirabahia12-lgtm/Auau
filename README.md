local player = game.Players.LocalPlayer
local RunService = game:GetService("RunService")

RunService.RenderStepped:Connect(function()
	if not player.Character or not player.Character:FindFirstChild("HumanoidRootPart") then return end

	for _, p in pairs(game.Players:GetPlayers()) do
		if p ~= player and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
			local dist = (player.Character.HumanoidRootPart.Position - p.Character.HumanoidRootPart.Position).Magnitude
			print(p.Name .. " | Distância: " .. math.floor(dist))
		end
	end
end)
game.Players.PlayerAdded:Connect(function(player)
	player.CharacterAdded:Connect(function(char)
		for _, part in pairs(char:GetChildren()) do
			if part:IsA("BasePart") then
				local box = Instance.new("SelectionBox")
				box.Adornee = part
				box.LineThickness = 0.03
				box.Color3 = Color3.fromRGB(255, 0, 0)
				box.Parent = part
			end
		end
	end)
end)
local RunService = game:GetService("RunService")
local camera = workspace.CurrentCamera

RunService.RenderStepped:Connect(function()
	for _, p in pairs(game.Players:GetPlayers()) do
		if p.Character and p.Character:FindFirstChild("Head") then
			local head = p.Character.Head
			local pos, onScreen = camera:WorldToViewportPoint(head.Position)

			if onScreen then
				-- aqui você desenha um ponto/círculo na tela
				-- NÃO move a mira automaticamente
			end
		end
	end
end)
