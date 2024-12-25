local plr = game.Players.LocalPlayer
local ReplicatedStorage = game:GetService('ReplicatedStorage')
local RunService = game:GetService('RunService')
local VirtualUser = game:GetService('VirtualUser')

local bonusRegion = workspace:FindFirstChild('ServerValues')
                 and workspace.ServerValues:FindFirstChild('ServerBonus')
                 and workspace.ServerValues.ServerBonus:FindFirstChild('CurrentRegionBonus')

local badRegionPos = Vector3.new(50000, 50000, 30000)
local firstTimeTeleportedRegions = false

plr.Idled:Connect(function()
    VirtualUser:CaptureController()
    VirtualUser:ClickButton2(Vector2.new())
end)

if bonusRegion then
    task.spawn(function()
        if not firstTimeTeleportedRegions then
            firstTimeTeleportedRegions = true
            for _, part in pairs(ReplicatedStorage.Regions:GetDescendants()) do
                if part:IsA('Part') then
                    part.CFrame = CFrame.new(badRegionPos)
                end
            end
        end

        RunService.Heartbeat:Connect(function()
            if plr.Character
                and plr.Character:FindFirstChild('PrimaryPart')
                and plr.Character:FindFirstChild('Stats')
                and plr.Character.Stats:FindFirstChild('CurrentRegion') then

                local currentRegionValue = plr.Character.Stats.CurrentRegion.Value
                local targetRegionName = bonusRegion.Value

                if currentRegionValue ~= targetRegionName then
                    local regionName = targetRegionName
                    local regionPart = ReplicatedStorage.Regions:FindFirstChild(regionName)
                                    and ReplicatedStorage.Regions[regionName]:FindFirstChild('Region')

                    if regionPart then
                        while bonusRegion.Value == regionName do
                            if plr.Character and plr.Character.PrimaryPart then
                                regionPart.CFrame = CFrame.new(plr.Character.PrimaryPart.Position)
                            else
                                break
                            end
                            RunService.Heartbeat:Wait()
                        end
                        regionPart.CFrame = CFrame.new(badRegionPos)
                    end
                end
            end
        end)
    end)
end
