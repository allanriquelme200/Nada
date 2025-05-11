-- Hub Completo para Florianópolis RP

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")
local Workspace = game:GetService("Workspace")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- GUI Setup
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "FloripaRP_Hub"
local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0, 350, 0, 500)
MainFrame.Position = UDim2.new(0.5, -175, 0.5, -250)
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.BorderSizePixel = 0

local UIListLayout = Instance.new("UIListLayout", MainFrame)
UIListLayout.Padding = UDim.new(0, 5)
UIListLayout.FillDirection = Enum.FillDirection.Vertical
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder

local function createButton(name, callback)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(1, -10, 0, 40)
    button.Position = UDim2.new(0, 5, 0, 0)
    button.Text = name
    button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    button.TextColor3 = Color3.new(1, 1, 1)
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 18
    button.MouseButton1Click:Connect(callback)
    button.Parent = MainFrame
    return button
end

-- Funções Exploit (Exemplos)
createButton("Aimbot Ativar", function()
    -- Aimbot (Exemplo simplificado)
    local Camera = workspace.CurrentCamera
    local FOV_RADIUS = 100
    local TARGET_PART = "Head"
    local function getClosestTarget()
        local closest = nil
        local shortestDistance = FOV_RADIUS
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild(TARGET_PART) then
                local part = player.Character:FindFirstChild(TARGET_PART)
                local pos, onScreen = Camera:WorldToViewportPoint(part.Position)
                if onScreen then
                    local dist = (Vector2.new(pos.X, pos.Y) - Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)).Magnitude
                    if dist < shortestDistance then
                        shortestDistance = dist
                        closest = part
                    end
                end
            end
        end
        return closest
    end
    
    RunService.RenderStepped:Connect(function()
        local target = getClosestTarget()
        if target then
            Camera.CFrame = CFrame.new(Camera.CFrame.Position, target.Position)
        end
    end)
end)

createButton("Auto Farm", function()
    -- Exemplo simples de auto farm
    local farmLocation = Vector3.new(100, 10, 200)  -- Altere para a posição de farm real
    LocalPlayer.Character:MoveTo(farmLocation)
    wait(5)  -- Tempo de espera para a interação, ajuste conforme o jogo
    -- Simular a interação
    -- Você pode adicionar funções que simulam clicar em objetos ou coletar recursos.
end)

createButton("Dupe Itens", function()
    -- Função de duplicação (exemplo)
    local inventory = LocalPlayer:FindFirstChild("Backpack") or LocalPlayer:FindFirstChild("PlayerScripts") -- Modifique conforme o jogo
    local itemToDupe = inventory:FindFirstChild("ItemName") -- Altere para o nome do item
    if itemToDupe then
        local newItem = itemToDupe:Clone()
        newItem.Parent = inventory
    end
end)

createButton("Dinheiro Infinito", function()
    -- Exemplo de adicionar dinheiro infinito (alterar conforme o sistema de dinheiro do jogo)
    local moneySystem = LocalPlayer:FindFirstChild("Leaderstats"):FindFirstChild("Money")
    if moneySystem then
        moneySystem.Value = math.huge
    end
end)

createButton("Speed Hack x2", function()
    local humanoid = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
    if humanoid then
        humanoid.WalkSpeed = 32  -- Aumenta a velocidade para 2x
    end
end)

createButton("Invisibilidade", function()
    for _, part in ipairs(LocalPlayer.Character:GetDescendants()) do
        if part:IsA("BasePart") and part.Name ~= "HumanoidRootPart" then
            part.Transparency = 1
            part.CanCollide = false
        end
    end
end)

createButton("Teleportar para Hospital", function()
    LocalPlayer.Character:MoveTo(Vector3.new(208, 17, -127)) -- Altere as coordenadas para o hospital real
end)

createButton("Teleportar para Garagem", function()
    LocalPlayer.Character:MoveTo(Vector3.new(321, 18, 70)) -- Altere as coordenadas para a garagem real
end)

createButton("Resetar Personagem", function()
    LocalPlayer:LoadCharacter()
end)

print("[Floripa RP Hub] Carregado com sucesso.")
