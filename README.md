local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")

local targetPlayer

function findClosestPlayer()
    local closestPlayer = nil
    local closestDistance = math.huge

    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            local character = player.Character
            if character and character:FindFirstChild("Head") then
                local distance = (character.Head.Position - LocalPlayer.Character.Head.Position).Magnitude
                if distance < closestDistance then
                    closestPlayer = player
                    closestDistance = distance
                end
            end
        end
    end

    return closestPlayer
end

RunService.RenderStepped:Connect(function()
    targetPlayer = findClosestPlayer()
    if targetPlayer then
        -- Replace this line with your desired action
        print("Locked onto:", targetPlayer.Name)
    end
end)
