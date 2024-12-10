-- Script for an advanced farming panel in Roblox

local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local PlantButton = Instance.new("TextButton")
local HarvestButton = Instance.new("TextButton")
local SeedSelector = Instance.new("TextBox")

ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

Frame.Size = UDim2.new(0.3, 0, 0.4, 0)
Frame.Position = UDim2.new(0.35, 0, 0.3, 0)
Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Frame.Parent = ScreenGui

SeedSelector.Size = UDim2.new(0.8, 0, 0.2, 0)
SeedSelector.Position = UDim2.new(0.1, 0, 0.1, 0)
SeedSelector.PlaceholderText = "Enter seed type (e.g., Oats)"
SeedSelector.Parent = Frame

PlantButton.Size = UDim2.new(0.8, 0, 0.2, 0)
PlantButton.Position = UDim2.new(0.1, 0, 0.4, 0)
PlantButton.Text = "Prepare and Plant"
PlantButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
PlantButton.Parent = Frame

HarvestButton.Size = UDim2.new(0.8, 0, 0.2, 0)
HarvestButton.Position = UDim2.new(0.1, 0, 0.7, 0)
HarvestButton.Text = "Harvest"
HarvestButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
HarvestButton.Parent = Frame

local function prepareSoil()
    local soil = Instance.new("Part")
    soil.Size = Vector3.new(4, 1, 4)
    soil.Anchored = true
    soil.Position = Vector3.new(0, 0.5, 0)
    soil.BrickColor = BrickColor.new("Brown")
    soil.Parent = workspace
    return soil
end

local function createPlant(seedType)
    local plant = Instance.new("Part")
    plant.Size = Vector3.new(2, 2, 2)
    plant.Anchored = true
    plant.Position = Vector3.new(0, 1.5, 0)
    plant.Name = seedType
    plant.BrickColor = BrickColor.new("Green")
    plant.Parent = workspace
    return plant
end

local function growPlant(plant)
    for i = 1, 5 do
        plant.Size = plant.Size + Vector3.new(0, 1, 0)
        wait(1)
    end
end

local function harvestPlant(plant)
    plant:Destroy()
    print("Plant harvested!")
end

PlantButton.MouseButton1Click:Connect(function()
    local seedType = SeedSelector.Text
    if seedType ~= "" then
        local soil = prepareSoil()
        local plant = createPlant(seedType)
        growPlant(plant)
    else
        print("Please enter a seed type.")
    end
end)

HarvestButton.MouseButton1Click:Connect(function()
    for _, plant in pairs(workspace:GetChildren()) do
        if plant:IsA("Part") and plant.Name ~= "Terrain" then
            harvestPlant(plant)
        end
    end
end)

