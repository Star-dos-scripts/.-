--Carregar biblioteca
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()

local Window = Fluent:CreateWindow({
    Title = "LOLKID 2.0 " .. Fluent.Version,
    TabWidth = 160, Size = UDim2.fromOffset(580, 460), Theme = "Dark"
})

local Tabs = {
    Main = Window:AddTab({ Title = "PLAYER" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}
--parÃ¡grafo
Tabs.Main:AddParagraph({ Title = "explâ‚©", Content = "This is a paragraph.\nSecond line!" })

--botÃµes
Tabs.Main:AddButton({ Title = "fly", Callback = function() local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local flying = false
local speed = 50

local UIS = game:GetService("UserInputService")
local runService = game:GetService("RunService")

local bodyGyro = Instance.new("BodyGyro")
local bodyVelocity = Instance.new("BodyVelocity")

function startFly()
	if flying then return end
	flying = true

	bodyGyro.P = 9e4
	bodyGyro.Parent = char.HumanoidRootPart
	bodyGyro.MaxTorque = Vector3.new(9e9, 9e9, 9e9)
	bodyGyro.CFrame = char.HumanoidRootPart.CFrame

	bodyVelocity.Velocity = Vector3.zero
	bodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9)
	bodyVelocity.Parent = char.HumanoidRootPart

	runService:BindToRenderStep("Fly", Enum.RenderPriority.Input.Value, function()
		bodyGyro.CFrame = workspace.CurrentCamera.CFrame
		bodyVelocity.Velocity = workspace.CurrentCamera.CFrame.LookVector * speed
	end)
end

function stopFly()
	flying = false
	bodyGyro:Destroy()
	bodyVelocity:Destroy()
	runService:UnbindFromRenderStep("Fly")
end

script.Parent:WaitForChild("Fly").MouseButton1Click:Connect(startFly)
script.Parent:WaitForChild("Stop").MouseButton1Click:Connect(stopFly)
 end })

Tabs.Main:AddButton({ Title = "walkspeed", Callback = function() local player = game.Players.LocalPlayer
local speedButton = script.Parent:WaitForChild("TextButton")

local normalSpeed = 16
local superSpeed = 100
local isFast = false

speedButton.MouseButton1Click:Connect(function()
	local character = player.Character or player.CharacterAdded:Wait()
	local humanoid = character:FindFirstChildOfClass("Humanoid")

	if humanoid then
		if not isFast then
			humanoid.WalkSpeed = superSpeed
			speedButton.Text = "Velocidade Normal"
		else
			humanoid.WalkSpeed = normalSpeed
			speedButton.Text = "Super Velocidade"
		end
		isFast = not isFast
	end
end)
 end })

Tabs.Main:AddButton({ Title = "inf jump", Callback = function() -- Infinite Jump Script
-- Funciona segurando a tecla de pulo (barra de espaÃ§o)

local UserInputService = game:GetService("UserInputService")
local player = game:GetService("Players").LocalPlayer
local humanoid = player.Character:WaitForChild("Humanoid")

UserInputService.JumpRequest:Connect(function()
    humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
end) end })

Window:SelectTab(1)
Fluent:Notify({ Title = "Fluent", Content = "The script has been loaded." })



















































































