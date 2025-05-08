-- Interface
local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "AnimePowerUI"

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 220, 0, 300)
frame.Position = UDim2.new(0, 100, 0, 100)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.BorderSizePixel = 0

local UIListLayout = Instance.new("UIListLayout", frame)
UIListLayout.Padding = UDim.new(0, 10)
UIListLayout.FillDirection = Enum.FillDirection.Vertical
UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder

local function criarBotao(nome, func)
	local btn = Instance.new("TextButton", frame)
	btn.Size = UDim2.new(0, 200, 0, 40)
	btn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
	btn.TextColor3 = Color3.fromRGB(255, 255, 255)
	btn.Font = Enum.Font.SourceSansBold
	btn.TextSize = 18
	btn.Text = nome
	btn.MouseButton1Click:Connect(func)
end

-- Variáveis de controle
local autoFarm = false
local autoDungeon = false
local autoNPC = false
local autoAura = false

-- Funções simuladas
local function loopAutoFarm()
	while autoFarm do
		for _, npc in pairs(workspace:GetChildren()) do
			if npc:IsA("Model") and npc:FindFirstChild("Humanoid") and npc.Name == "Dummy" then
				player.Character:MoveTo(npc.Position + Vector3.new(0, 2, 0))
				npc.Humanoid:TakeDamage(10)
			end
		end
		wait(1)
	end
end

local function loopAutoDungeon()
	while autoDungeon do
		print("Auto Dungeon rodando...")
		wait(2)
	end
end

local function loopAutoNPC()
	while autoNPC do
		print("Auto NPC rodando...")
		wait(2)
	end
end

local function loopAutoAura()
	while autoAura do
		print("Auto Aura rodando...")
		wait(2)
	end
end

-- Criação dos botões com funções
criarBotao("Auto Farm", function()
	autoFarm = not autoFarm
	if autoFarm then spawn(loopAutoFarm) end
end)

criarBotao("Auto Dungeon", function()
	autoDungeon = not autoDungeon
	if autoDungeon then spawn(loopAutoDungeon) end
end)

criarBotao("Auto NPC", function()
	autoNPC = not autoNPC
	if autoNPC then spawn(loopAutoNPC) end
end)

criarBotao("Auto Aura", function()
	autoAura = not autoAura
	if autoAura then spawn(loopAutoAura) end
end)

criarBotao("Auto Tudo", function()
	autoFarm, autoDungeon, autoNPC, autoAura = true, true, true, true
	spawn(loopAutoFarm)
	spawn(loopAutoDungeon)
	spawn(loopAutoNPC)
	spawn(loopAutoAura)
end)# Uwajkwwkw
