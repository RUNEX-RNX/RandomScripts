-- ts file was generated at discord.gg/25ms

local _UserInputService = game:GetService('UserInputService')
local _Players = game:GetService('Players')
local _ = game.Players.LocalPlayer
local _ScreenGui = Instance.new('ScreenGui')
local _Frame = Instance.new('Frame')
local _TextButton = Instance.new('TextButton')
local _TextButton2 = Instance.new('TextButton')
local _UIAspectRatioConstraint = Instance.new('UIAspectRatioConstraint')
local _TextButton3 = Instance.new('TextButton')

game:GetService('StarterGui'):SetCore('SendNotification', {
    Title = 'Combos loaded',
    Text = "Doesn't work on dummy",
    Duration = 2.6,
})

_ScreenGui.Parent = _Players.LocalPlayer:WaitForChild('PlayerGui')
_ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
_Frame.Parent = _ScreenGui
_Frame.AnchorPoint = Vector2.new(0.5, 0.5)
_Frame.BackgroundColor3 = Color3.fromRGB(145, 145, 145)
_Frame.BorderColor3 = Color3.fromRGB(0, 0, 0)
_Frame.Position = UDim2.new(0.15, 0, 0.42, 0)
_Frame.Size = UDim2.new(0.15, 0, 0.4, 0)
_Frame.Visible = true
_TextButton.Parent = _Frame
_TextButton.BackgroundColor3 = Color3.fromRGB(145, 145, 145)
_TextButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
_TextButton.Size = UDim2.new(1, 0, 0.21, 0)
_TextButton.Font = Enum.Font.SourceSans
_TextButton.Text = 'Kyoto'
_TextButton.TextColor3 = Color3.fromRGB(0, 0, 0)
_TextButton.TextSize = 15
_TextButton.TextWrapped = true
_TextButton2.Parent = _Frame
_TextButton2.BackgroundColor3 = Color3.fromRGB(145, 145, 145)
_TextButton2.BorderColor3 = Color3.fromRGB(0, 0, 0)
_TextButton2.Position = UDim2.new(0, 0, 0.21, 0)
_TextButton2.Size = UDim2.new(1, 0, 0.2, 0)
_TextButton2.Font = Enum.Font.SourceSans
_TextButton2.Text = 'Lordheaven'
_TextButton2.TextColor3 = Color3.fromRGB(0, 0, 0)
_TextButton2.TextSize = 15
_TextButton2.TextWrapped = true
_UIAspectRatioConstraint.Parent = _Frame
_UIAspectRatioConstraint.AspectRatio = 0.79
_TextButton3.Parent = _ScreenGui
_TextButton3.BackgroundColor3 = Color3.fromRGB(145, 145, 145)
_TextButton3.BorderColor3 = Color3.fromRGB(0, 0, 0)
_TextButton3.Position = UDim2.new(0, 0, 0.35, 0)
_TextButton3.Size = UDim2.new(0.05, 0, 0.08, 0)
_TextButton3.Font = Enum.Font.SourceSans
_TextButton3.Text = 'Close'
_TextButton3.TextColor3 = Color3.fromRGB(0, 0, 0)
_TextButton3.TextScaled = true
_TextButton3.TextSize = 14
_TextButton3.TextWrapped = true
_TextButton3.Draggable = true

local u9 = true

local function u11(p10)
    if p10 then
        _Frame.Visible = true

        _Frame:TweenSize(UDim2.new(0.15, 0, 0.4, 0), Enum.EasingDirection.Out, Enum.EasingStyle.Quint, 0.2, true)
    else
        _Frame:TweenSize(UDim2.new(0, 0, 0, 0), Enum.EasingDirection.In, Enum.EasingStyle.Quint, 0.15, true, function()
            _Frame.Visible = false
        end)
    end
end

_TextButton3.MouseButton1Click:Connect(function()
    u9 = not u9

    u11(u9)

    _TextButton3.Text = u9 and 'Close' or 'Open'
end)

local u12 = false
local u13 = nil
local u14 = nil
local u15 = nil

_Frame.InputBegan:Connect(function(p16)
    if p16.UserInputType == Enum.UserInputType.MouseButton1 then
        u12 = true
        u14 = p16.Position
        u15 = _Frame.Position
    end
end)
_Frame.InputChanged:Connect(function(p17)
    if p17.UserInputType == Enum.UserInputType.MouseMovement then
        u13 = p17
    end
end)
_UserInputService.InputChanged:Connect(function(p18)
    if p18 == u13 and u12 then
        local v19 = p18.Position - u14

        _Frame.Position = UDim2.new(u15.X.Scale, u15.X.Offset + v19.X, u15.Y.Scale, u15.Y.Offset + v19.Y)
    end
end)
_Frame.InputEnded:Connect(function(p20)
    if p20.UserInputType == Enum.UserInputType.MouseButton1 then
        u12 = false
    end
end)

getgenv().Requires4M1 = getgenv().Requires4M1 or true

local function u22(p21)
    game:GetService('Players').LocalPlayer.Character.Communicate:FireServer(unpack(p21))
end
local function u25(p23, p24)
    game:GetService('VirtualInputManager'):SendKeyEvent(p23, p24, false, game)
end
local function u29(p26)
    local _CurrentCamera = game.Workspace.CurrentCamera
    local v28 = _CurrentCamera.CFrame.Position + _CurrentCamera.CFrame.RightVector * p26

    _CurrentCamera.CFrame = CFrame.new(v28, _CurrentCamera.CFrame.Position + _CurrentCamera.CFrame.LookVector)
end

local _StarterGui = game:GetService('StarterGui')
local _LocalPlayer = game:GetService('Players').LocalPlayer

local function u33()
    local v32 = game:GetService('Stats').Network.ServerStatsItem['Data Ping']:GetValue()

    return math.floor(v32 % 1000)
end
local function u36(p34, p35)
    _StarterGui:SetCore('SendNotification', {
        Title = 'Ping Check',
        Text = 'Your ping: ' .. p34 .. ' ms | Delay: ' .. p35,
        Duration = 3,
    })
end
local function u47()
    local v37 = u33()
    local v38 = 2.38

    if 130 <= v37 and v37 <= 190 then
        v38 = 2.42
    elseif 191 <= v37 and v37 <= 320 then
        v38 = 2.5
    elseif v37 > 321 then
        _StarterGui:SetCore('SendNotification', {
            Title = 'Ping Check',
            Text = 'Your ping is too high for Kyoto (' .. v37 .. ' ms)',
            Duration = 2.6,
        })

        return
    end

    u36(v37, v38)

    if getgenv().Requires4M1 then
        u25(true, Enum.KeyCode.D)
        u25(false, Enum.KeyCode.Q)
        u25(true, Enum.KeyCode.Q)
        u25(false, Enum.KeyCode.D)
        u29(13)
    end

    local v39 = {}
    local v40 = {
        Tool = _LocalPlayer.Backpack:FindFirstChild('Flowing Water'),
        Goal = 'Console Move',
    }

    v39[1] = v40

    u22(v39)
    wait(1.7)

    local _Humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass('Humanoid')

    if _Humanoid then
        _Humanoid = _Humanoid:FindFirstChildWhichIsA('Animator')
    end

    local v42 = _Humanoid and _Humanoid:GetPlayingAnimationTracks()[1]

    if v42 then
        v42 = _Humanoid:GetPlayingAnimationTracks()[1].Animation.AnimationId == 'rbxassetid://12273188754'
    end
    if v42 then
        wait(v38 - 1.70001)
        u25(true, Enum.KeyCode.D)
        u25(false, Enum.KeyCode.Q)
        u25(true, Enum.KeyCode.Q)
        u25(false, Enum.KeyCode.D)
        u29(12)

        local v43 = {}
        local v44 = {
            Tool = _LocalPlayer.Backpack:FindFirstChild('Lethal Whirlwind Stream'),
            Goal = 'Console Move',
        }

        v43[1] = v44

        u22(v43)
        wait(1)

        local _Humanoid2 = game.Players.LocalPlayer.Character:FindFirstChildOfClass('Humanoid')

        if _Humanoid2 then
            _Humanoid2 = _Humanoid2:FindFirstChildWhichIsA('Animator')
        end

        local v46 = _Humanoid2 and _Humanoid2:GetPlayingAnimationTracks()[1]

        if v46 then
            v46 = _Humanoid2:GetPlayingAnimationTracks()[1].Animation.AnimationId == 'rbxassetid://12296113986'
        end
        if not v46 then
            _StarterGui:SetCore('SendNotification', {
                Title = 'Kyoto Notification',
                Text = 'Lethal Whirlwind Stream failed. Try again or check your ping',
                Duration = 2,
            })
        end
    else
        _StarterGui:SetCore('SendNotification', {
            Title = 'RUNEX Notification',
            Text = 'Flowing Water failed. Try again or check your ping',
            Duration = 2,
        })

        return
    end
end

_TextButton.MouseButton1Click:Connect(function()
    u47()
end)
_TextButton2.MouseButton1Click:Connect(function()
    local v48 = {
        {
            Tool = game:GetService('Players').LocalPlayer:WaitForChild('Backpack'):WaitForChild('Uppercut'),
            Goal = 'Console Move',
        },
    }

    game:GetService('Players').LocalPlayer.Character:WaitForChild('Communicate'):FireServer(unpack(v48))
    wait(1.57)
    u25(true, Enum.KeyCode.D)
    u25(false, Enum.KeyCode.Q)
    u25(true, Enum.KeyCode.Q)
    u25(false, Enum.KeyCode.D)
    u29(19)
    task.wait(0.33)
    game:GetService('Players').LocalPlayer.Character.Communicate:FireServer(unpack({
        {
            Goal = 'LeftClick',
            Mobile = true,
        },
    }))
    game:GetService('Players').LocalPlayer.Character.Communicate:FireServer(unpack({
        {
            Goal = 'LeftClickRelease',
            Mobile = true,
        },
    }))
    wait(0.25)

    local _LocalPlayer2 = game.Players.LocalPlayer
    local _Character = _LocalPlayer2.Character

    if not _Character then
        return
    end

    local _HumanoidRootPart = _Character:FindFirstChild('HumanoidRootPart')

    if not _HumanoidRootPart then
        return
    end

    local _huge = math.huge
    local v53, v54, v55 = pairs(game.Players:GetPlayers())
    local v56 = nil

    while true do
        local v57

        v55, v57 = v53(v54, v55)

        if v55 == nil then
            break
        end
        if v57 ~= _LocalPlayer2 and v57.Character and v57.Character:FindFirstChild('HumanoidRootPart') then
            local _Magnitude = (v57.Character.HumanoidRootPart.Position - _HumanoidRootPart.Position).Magnitude

            if _Magnitude < _huge then
                v56 = v57.Character
                _huge = _Magnitude
            end
        end
    end

    if v56 then
        local _Humanoid3 = v56:FindFirstChildOfClass('Humanoid')

        if _Humanoid3 then
            _Humanoid3 = v56:FindFirstChildOfClass('Humanoid'):FindFirstChildWhichIsA('Animator')
        end

        local v60 = false

        if _Humanoid3 then
            local v61, v62, v63 = pairs(_Humanoid3:GetPlayingAnimationTracks())

            while true do
                local v64

                v63, v64 = v61(v62, v63)

                if v63 == nil then
                    break
                end
                if v64.Animation.AnimationId == 'rbxassetid://10473654583' or (v64.Animation.AnimationId == 'rbxassetid://10473653782' or (v64.Animation.AnimationId == 'rbxassetid://10473655645' or v64.Animation.AnimationId == 'rbxassetid://10473655082')) then
                    v60 = true

                    break
                end
            end
        end
        if not v60 then
            game:GetService('StarterGui'):SetCore('SendNotification', {
                Title = 'Lordheaven Notification',
                Text = 'Failed to land Uppercut catch',
                Duration = 2,
            })

            return
        end
    end

    task.wait(0.45)

    local v65 = {
        {
            Tool = game:GetService('Players').LocalPlayer:WaitForChild('Backpack'):WaitForChild('Shove'),
            Goal = 'Console Move',
        },
    }

    game:GetService('Players').LocalPlayer.Character:WaitForChild('Communicate'):FireServer(unpack(v65))
    task.wait(0.485)
    game:GetService('Players').LocalPlayer.Character.Communicate:FireServer(unpack({
        {
            Goal = 'LeftClick',
            Mobile = true,
        },
    }))
    u25(true, Enum.KeyCode.S)
    game:GetService('Players').LocalPlayer.Character.Communicate:FireServer(unpack({
        {
            Goal = 'LeftClickRelease',
            Mobile = true,
        },
    }))
    task.wait(0.23)
    u25(false, Enum.KeyCode.S)
    task.wait(0.45)
    u25(true, Enum.KeyCode.Q)
    u25(false, Enum.KeyCode.Q)
    wait(0.84)

    local _LocalPlayer3 = game.Players.LocalPlayer
    local _Character2 = _LocalPlayer3.Character

    if not _Character2 then
        return
    end

    local _HumanoidRootPart2 = _Character2:FindFirstChild('HumanoidRootPart')

    if not _HumanoidRootPart2 then
        return
    end

    local _huge2 = math.huge
    local v70, v71, v72 = pairs(game.Players:GetPlayers())
    local v73 = nil

    while true do
        local v74

        v72, v74 = v70(v71, v72)

        if v72 == nil then
            break
        end
        if v74 ~= _LocalPlayer3 and v74.Character and v74.Character:FindFirstChild('HumanoidRootPart') then
            local _Magnitude2 = (v74.Character.HumanoidRootPart.Position - _HumanoidRootPart2.Position).Magnitude

            if _Magnitude2 < _huge2 then
                v73 = v74.Character
                _huge2 = _Magnitude2
            end
        end
    end

    if v73 then
        local _Humanoid4 = v73:FindFirstChildOfClass('Humanoid')

        if _Humanoid4 then
            _Humanoid4 = v73:FindFirstChildOfClass('Humanoid'):FindFirstChildWhichIsA('Animator')
        end

        local v77 = false

        if _Humanoid4 then
            local v78, v79, v80 = pairs(_Humanoid4:GetPlayingAnimationTracks())

            while true do
                local v81

                v80, v81 = v78(v79, v80)

                if v80 == nil then
                    break
                end
                if v81.Animation.AnimationId == 'rbxassetid://10473654583' or (v81.Animation.AnimationId == 'rbxassetid://10473653782' or (v81.Animation.AnimationId == 'rbxassetid://10473655645' or v81.Animation.AnimationId == 'rbxassetid://10473655082')) then
                    v77 = true

                    break
                end
            end
        end
        if not v77 then
            game:GetService('StarterGui'):SetCore('SendNotification', {
                Title = 'Lordheaven Notification',
                Text = 'Failed to land Shove dash',
                Duration = 2,
            })

            return
        end
    end

    wait(0.1)
    game:GetService('Players').LocalPlayer.Character.Communicate:FireServer(unpack({
        {
            Goal = 'LeftClick',
            Mobile = true,
        },
    }))
    wait(0.7)
    game:GetService('Players').LocalPlayer.Character.Communicate:FireServer(unpack({
        {
            Goal = 'LeftClickRelease',
            Mobile = true,
        },
    }))
    wait(0.15)

    local v82 = {
        {
            Tool = game:GetService('Players').LocalPlayer:WaitForChild('Backpack'):WaitForChild('Consecutive Punches'),
            Goal = 'Console Move',
        },
    }

    game:GetService('Players').LocalPlayer.Character:WaitForChild('Communicate'):FireServer(unpack(v82))
    wait(1.5)
    game:GetService('Players').LocalPlayer.Character.Communicate:FireServer(unpack({
        {
            Goal = 'LeftClick',
            Mobile = true,
        },
    }))
    game:GetService('Players').LocalPlayer.Character.Communicate:FireServer(unpack({
        {
            Goal = 'LeftClickRelease',
            Mobile = true,
        },
    }))
    wait(0.35)

    local v83 = {
        {
            Tool = game:GetService('Players').LocalPlayer:WaitForChild('Backpack'):WaitForChild('Normal Punch'),
            Goal = 'Console Move',
        },
    }

    game:GetService('Players').LocalPlayer.Character:WaitForChild('Communicate'):FireServer(unpack(v83))
end)
