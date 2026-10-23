if not game:IsLoaded() then game.Loaded:Wait() end

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local VirtualUser = game:GetService("VirtualUser")
local TweenService = game:GetService("TweenService")
local GuiService = game:GetService("GuiService")
local TeleportService = game:GetService("TeleportService")

local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

local gs = getgenv and getgenv() or _G
if gs.CandyFarmUnload then gs.CandyFarmUnload() end

local Theme = {
    Bg = Color3.fromRGB(16, 12, 20),
    Surface = Color3.fromRGB(26, 20, 32),
    SurfaceAlt = Color3.fromRGB(36, 28, 46),
    Accent = Color3.fromRGB(255, 125, 45),
    AccentSoft = Color3.fromRGB(255, 165, 90),
    AccentDark = Color3.fromRGB(180, 80, 25),
    Text = Color3.fromRGB(248, 242, 238),
    TextDim = Color3.fromRGB(155, 145, 165),
    TextMuted = Color3.fromRGB(105, 95, 115),
    Border = Color3.fromRGB(50, 40, 62),
    BorderLight = Color3.fromRGB(75, 60, 88),
    Success = Color3.fromRGB(95, 215, 125),
    Danger = Color3.fromRGB(235, 80, 80),
    Track = Color3.fromRGB(60, 50, 72),
}

local Candy = {
    { DataName = "CandyOrange", Icon = "rbxassetid://7781288646" },
    { DataName = "CandyPurple", Icon = "rbxassetid://7781287748" },
    { DataName = "CandyBlue", Icon = "rbxassetid://7781285156" },
    { DataName = "CandyPink", Icon = "rbxassetid://7781284023" },
    { DataName = "CandyRed", Icon = "rbxassetid://7781250539" },
}

local config = { AntiAfk = true, HidePopups = true }
local Runtime = { Farming = false, Root = nil, Claimed = {}, Reconnecting = false, Running = true }
local Session = { Candy = {}, Houses = 0, Mark = nil }

local hiddenPopup = nil
local RefreshUI

task.spawn(function()
    local itemGained = PlayerGui:WaitForChild("ItemGained")
    local display = itemGained:WaitForChild("DisplayGainedItem")
    hiddenPopup = display:WaitForChild("LocalScript")
end)

task.spawn(function()
    local dataFolder = LocalPlayer:WaitForChild("Data")
    local before = {}
    for _, candy in ipairs(Candy) do
        local v = dataFolder:FindFirstChild(candy.DataName)
        if v then
            before[candy.DataName] = v.Value
            v:GetPropertyChangedSignal("Value"):Connect(function()
                local delta = v.Value - before[candy.DataName]
                if delta > 0 then
                    Session.Candy[candy.DataName] = (Session.Candy[candy.DataName] or 0) + delta
                    if RefreshUI then RefreshUI() end
                end
                before[candy.DataName] = v.Value
            end)
        end
    end
end)

LocalPlayer.CharacterAdded:Connect(function(char)
    Runtime.Root = char:WaitForChild("HumanoidRootPart")
end)
if LocalPlayer.Character then
    Runtime.Root = LocalPlayer.Character:WaitForChild("HumanoidRootPart")
end

LocalPlayer.Idled:Connect(function()
    if config.AntiAfk then
        VirtualUser:CaptureController()
        VirtualUser:ClickButton2(Vector2.new())
    end
end)

GuiService.ErrorMessageChanged:Connect(function()
    local msg = GuiService:GetErrorMessage()
    local lower = string.lower(msg)
    if lower:find("disconnectclientinitiated", 1, true) then return end
    if not (lower:find("267", 1, true) or lower:find("disconnect", 1, true)
        or lower:find("connection", 1, true) or lower:find("network", 1, true)) then return end
    if Runtime.Reconnecting then return end
    Runtime.Reconnecting = true
    Runtime.Farming = false

    queue_on_teleport("if not game:IsLoaded() then game.Loaded:Wait() end getgenv().CandyFarmFromHop = true loadstring(game:HttpGet('https://raw.githubusercontent.com/Fantom233/BABFT/refs/heads/main/CandyFarm.lua'))()")

    task.spawn(function()
        while Runtime.Reconnecting do
            TeleportService:Teleport(537413528, LocalPlayer)
            task.wait(5)
        end
    end)
end)

local function HidePopup()
    if not hiddenPopup then return end
    hiddenPopup.Disabled = config.HidePopups
    if config.HidePopups then
        for _, child in ipairs(hiddenPopup.Parent:GetChildren()) do
            if child:IsA("ScreenGui") then child.Enabled = false end
        end
    end
end

local function ClaimAll()
    local root = Runtime.Root
    local houses = workspace:FindFirstChild("Houses")
    if not root or not houses then return 0 end

    local count = 0

    for _, house in ipairs(houses:GetChildren()) do
        if not Runtime.Claimed[house] then
            local door = house:FindFirstChild("DoorInnerTouch", true)
            if door then
                local savedCFrame = door.CFrame
                door.CFrame = root.CFrame
                door.CanCollide = false
                door.Transparency = 1
                firetouchinterest(root, door, 0)
                firetouchinterest(root, door, 1)
                task.delay(0.05, function()
                    if door.Parent then
                        door.CFrame = savedCFrame
                    end
                end)
                Runtime.Claimed[house] = true
                count = count + 1
            end
            local hand = house:FindFirstChild("GiantHand")
            if hand then hand:Destroy() end
        end
    end

    if count > 0 then
        Session.Houses = Session.Houses + count
        HidePopup()
        if RefreshUI then RefreshUI() end
    end

    return count
end

local function StartFarm()
    if Runtime.Farming then return end
    Runtime.Farming = true
    Session.Mark = Session.Mark or os.time()
    Runtime.Claimed = {}

    task.spawn(function()
        while Runtime.Running and Runtime.Farming do
            local claimed = ClaimAll()
            if claimed == 0 then
                task.wait(0.15)
            end
        end
    end)

    if RefreshUI then RefreshUI() end
end

local function StopFarm()
    Runtime.Farming = false
    if RefreshUI then RefreshUI() end
end

local function New(class, props, children)
    local inst = Instance.new(class)
    for k, v in pairs(props) do inst[k] = v end
    for _, child in ipairs(children or {}) do child.Parent = inst end
    return inst
end

local viewport = workspace.CurrentCamera.ViewportSize
local width = math.clamp(math.floor(viewport.X / 8), 320, 380)

local screen = New("ScreenGui", {
    Name = "CandyFarm2026",
    ResetOnSpawn = false,
    ZIndexBehavior = Enum.ZIndexBehavior.Sibling,
    DisplayOrder = 100,
    IgnoreGuiInset = false,
    Parent = PlayerGui,
})

local main = New("Frame", {
    Size = UDim2.fromOffset(width, 0),
    AutomaticSize = Enum.AutomaticSize.Y,
    BackgroundColor3 = Theme.Bg,
    BackgroundTransparency = 1,
    BorderSizePixel = 0,
    Parent = screen,
}, {
    New("UICorner", { CornerRadius = UDim.new(0, 16) }),
    New("UIStroke", { Color = Theme.Border, Thickness = 1, Transparency = 0.3 }),
    New("UIListLayout", { SortOrder = Enum.SortOrder.LayoutOrder }),
    New("UIGradient", {
        Color = ColorSequence.new{
            ColorSequenceKeypoint.new(0, Theme.Bg),
            ColorSequenceKeypoint.new(1, Theme.Surface),
        },
        Rotation = 90,
    }),
})

local scale = New("UIScale", { Parent = main })

local header = New("Frame", {
    Size = UDim2.new(1, 0, 0, 58),
    BackgroundColor3 = Theme.Surface,
    BorderSizePixel = 0,
    LayoutOrder = 1,
    Parent = main,
}, { New("UICorner", { CornerRadius = UDim.new(0, 16) }) })

New("Frame", {
    Size = UDim2.new(1, 0, 0, 16),
    Position = UDim2.new(0, 0, 1, -16),
    BackgroundColor3 = Theme.Surface,
    BorderSizePixel = 0,
    Parent = header,
})

New("UIGradient", {
    Color = ColorSequence.new{
        ColorSequenceKeypoint.new(0, Theme.Accent),
        ColorSequenceKeypoint.new(1, Theme.AccentDark),
    },
    Rotation = 90,
    Transparency = NumberSequence.new{
        NumberSequenceKeypoint.new(0, 0.82),
        NumberSequenceKeypoint.new(1, 0.95),
    },
    Parent = header,
})

New("Frame", {
    Size = UDim2.new(0, 3, 0, 24),
    Position = UDim2.fromOffset(16, 17),
    BackgroundColor3 = Theme.Accent,
    BorderSizePixel = 0,
    Parent = header,
}, { New("UICorner", { CornerRadius = UDim.new(1, 0) }) })

New("TextLabel", {
    Text = "Candy Farm",
    Font = Enum.Font.GothamBold,
    TextSize = 16,
    TextColor3 = Theme.Text,
    BackgroundTransparency = 1,
    TextXAlignment = Enum.TextXAlignment.Left,
    Size = UDim2.new(1, -120, 0, 20),
    Position = UDim2.fromOffset(28, 14),
    Parent = header,
})

local statusPill = New("Frame", {
    AnchorPoint = Vector2.new(0, 0.5),
    Position = UDim2.new(0, 28, 0, 40),
    Size = UDim2.fromOffset(0, 16),
    AutomaticSize = Enum.AutomaticSize.X,
    BackgroundTransparency = 1,
    Parent = header,
}, {
    New("UIListLayout", {
        FillDirection = Enum.FillDirection.Horizontal,
        VerticalAlignment = Enum.VerticalAlignment.Center,
        SortOrder = Enum.SortOrder.LayoutOrder,
        Padding = UDim.new(0, 6),
    }),
})

local statusDot = New("Frame", {
    Size = UDim2.fromOffset(7, 7),
    BackgroundColor3 = Theme.TextMuted,
    BorderSizePixel = 0,
    LayoutOrder = 1,
    Parent = statusPill,
}, { New("UICorner", { CornerRadius = UDim.new(1, 0) }) })

local statusText = New("TextLabel", {
    Text = "idle",
    Font = Enum.Font.GothamMedium,
    TextSize = 11,
    TextColor3 = Theme.TextDim,
    BackgroundTransparency = 1,
    TextXAlignment = Enum.TextXAlignment.Left,
    LayoutOrder = 2,
    AutomaticSize = Enum.AutomaticSize.X,
    Size = UDim2.fromOffset(0, 16),
    Parent = statusPill,
})

local function IconButton(x)
    return New("TextButton", {
        Text = "",
        Size = UDim2.fromOffset(28, 28),
        Position = UDim2.new(1, x, 0, 15),
        BackgroundColor3 = Theme.SurfaceAlt,
        BorderSizePixel = 0,
        AutoButtonColor = false,
        Parent = header,
    }, { New("UICorner", { CornerRadius = UDim.new(0, 8) }) })
end

local minBtn = IconButton(-66)
New("Frame", {
    AnchorPoint = Vector2.new(0.5, 0.5),
    Position = UDim2.fromScale(0.5, 0.5),
    Size = UDim2.fromOffset(10, 2),
    BackgroundColor3 = Theme.TextDim,
    BorderSizePixel = 0,
    Parent = minBtn,
}, { New("UICorner", { CornerRadius = UDim.new(1, 0) }) })

local closeBtn = IconButton(-34)
New("Frame", {
    AnchorPoint = Vector2.new(0.5, 0.5),
    Position = UDim2.fromScale(0.5, 0.5),
    Size = UDim2.fromOffset(11, 2),
    Rotation = 45,
    BackgroundColor3 = Theme.TextDim,
    BorderSizePixel = 0,
    Parent = closeBtn,
}, { New("UICorner", { CornerRadius = UDim.new(1, 0) }) })
New("Frame", {
    AnchorPoint = Vector2.new(0.5, 0.5),
    Position = UDim2.fromScale(0.5, 0.5),
    Size = UDim2.fromOffset(11, 2),
    Rotation = -45,
    BackgroundColor3 = Theme.TextDim,
    BorderSizePixel = 0,
    Parent = closeBtn,
}, { New("UICorner", { CornerRadius = UDim.new(1, 0) }) })

local body = New("Frame", {
    Size = UDim2.new(1, 0, 0, 0),
    AutomaticSize = Enum.AutomaticSize.Y,
    BackgroundTransparency = 1,
    LayoutOrder = 2,
    Parent = main,
}, {
    New("UIListLayout", { SortOrder = Enum.SortOrder.LayoutOrder, Padding = UDim.new(0, 10) }),
    New("UIPadding", {
        PaddingTop = UDim.new(0, 10),
        PaddingBottom = UDim.new(0, 14),
        PaddingLeft = UDim.new(0, 14),
        PaddingRight = UDim.new(0, 14),
    }),
})

local candyRow = New("Frame", {
    Size = UDim2.new(1, 0, 0, 60),
    BackgroundColor3 = Theme.Surface,
    BorderSizePixel = 0,
    LayoutOrder = 1,
    Parent = body,
}, {
    New("UICorner", { CornerRadius = UDim.new(0, 12) }),
    New("UIStroke", { Color = Theme.Border, Thickness = 1, Transparency = 0.4 }),
    New("UIPadding", {
        PaddingLeft = UDim.new(0, 10),
        PaddingRight = UDim.new(0, 10),
        PaddingTop = UDim.new(0, 10),
        PaddingBottom = UDim.new(0, 10),
    }),
})

New("UIListLayout", {
    FillDirection = Enum.FillDirection.Horizontal,
    VerticalAlignment = Enum.VerticalAlignment.Center,
    HorizontalAlignment = Enum.HorizontalAlignment.Center,
    HorizontalFlex = Enum.UIFlexAlignment.SpaceEvenly,
    Parent = candyRow,
})

local candyRefs = {}
for index, candy in ipairs(Candy) do
    local cell = New("Frame", {
        Size = UDim2.fromOffset(0, 40),
        AutomaticSize = Enum.AutomaticSize.X,
        BackgroundTransparency = 1,
        LayoutOrder = index,
        Parent = candyRow,
    }, {
        New("UIListLayout", {
            SortOrder = Enum.SortOrder.LayoutOrder,
            HorizontalAlignment = Enum.HorizontalAlignment.Center,
            Padding = UDim.new(0, 3),
        }),
    })
    New("ImageLabel", {
        Image = candy.Icon,
        BackgroundTransparency = 1,
        Size = UDim2.fromOffset(24, 24),
        ScaleType = Enum.ScaleType.Fit,
        LayoutOrder = 1,
        Parent = cell,
    })
    candyRefs[candy.DataName] = New("TextLabel", {
        Text = "0",
        Font = Enum.Font.GothamBold,
        TextSize = 14,
        TextColor3 = Theme.Text,
        BackgroundTransparency = 1,
        TextXAlignment = Enum.TextXAlignment.Center,
        Size = UDim2.fromOffset(28, 16),
        LayoutOrder = 2,
        Parent = cell,
    })
end

local statsCard = New("Frame", {
    Size = UDim2.new(1, 0, 0, 0),
    AutomaticSize = Enum.AutomaticSize.Y,
    BackgroundColor3 = Theme.Surface,
    BorderSizePixel = 0,
    LayoutOrder = 2,
    Parent = body,
}, {
    New("UICorner", { CornerRadius = UDim.new(0, 12) }),
    New("UIStroke", { Color = Theme.Border, Thickness = 1, Transparency = 0.4 }),
    New("UIPadding", {
        PaddingTop = UDim.new(0, 10),
        PaddingBottom = UDim.new(0, 10),
        PaddingLeft = UDim.new(0, 14),
        PaddingRight = UDim.new(0, 14),
    }),
    New("UIListLayout", { SortOrder = Enum.SortOrder.LayoutOrder, Padding = UDim.new(0, 8) }),
})

local function StatRow(order)
    return New("Frame", {
        Size = UDim2.new(1, 0, 0, 16),
        BackgroundTransparency = 1,
        LayoutOrder = order,
        Parent = statsCard,
    }, {
        New("UIListLayout", {
            FillDirection = Enum.FillDirection.Horizontal,
            VerticalAlignment = Enum.VerticalAlignment.Center,
            SortOrder = Enum.SortOrder.LayoutOrder,
        }),
    })
end

local function StatKey(text, parent)
    New("TextLabel", {
        Text = text,
        Font = Enum.Font.GothamBold,
        TextSize = 10,
        TextColor3 = Theme.TextMuted,
        BackgroundTransparency = 1,
        TextXAlignment = Enum.TextXAlignment.Left,
        Size = UDim2.fromOffset(64, 16),
        Parent = parent,
    })
end

local timeRow = StatRow(1)
StatKey("TIME", timeRow)
local timeVal = New("TextLabel", {
    Text = "00:00:00",
    Font = Enum.Font.GothamBold,
    TextSize = 13,
    TextColor3 = Theme.Text,
    BackgroundTransparency = 1,
    TextXAlignment = Enum.TextXAlignment.Left,
    Size = UDim2.new(1, -70, 0, 16),
    Parent = timeRow,
})

local housesRow = StatRow(2)
StatKey("HOUSES", housesRow)
local housesVal = New("TextLabel", {
    Text = "0",
    Font = Enum.Font.GothamBold,
    TextSize = 13,
    TextColor3 = Theme.Text,
    BackgroundTransparency = 1,
    TextXAlignment = Enum.TextXAlignment.Left,
    Size = UDim2.new(1, -70, 0, 16),
    Parent = housesRow,
})

local totalRow = StatRow(3)
StatKey("TOTAL", totalRow)
local totalVal = New("TextLabel", {
    Text = "0 candy",
    Font = Enum.Font.GothamBold,
    TextSize = 13,
    TextColor3 = Theme.Accent,
    BackgroundTransparency = 1,
    TextXAlignment = Enum.TextXAlignment.Left,
    Size = UDim2.new(1, -70, 0, 16),
    Parent = totalRow,
})

local togglesCard = New("Frame", {
    Size = UDim2.new(1, 0, 0, 0),
    AutomaticSize = Enum.AutomaticSize.Y,
    BackgroundColor3 = Theme.Surface,
    BorderSizePixel = 0,
    LayoutOrder = 3,
    Parent = body,
}, {
    New("UICorner", { CornerRadius = UDim.new(0, 12) }),
    New("UIStroke", { Color = Theme.Border, Thickness = 1, Transparency = 0.4 }),
    New("UIPadding", {
        PaddingTop = UDim.new(0, 6),
        PaddingBottom = UDim.new(0, 6),
        PaddingLeft = UDim.new(0, 10),
        PaddingRight = UDim.new(0, 10),
    }),
    New("UIListLayout", { SortOrder = Enum.SortOrder.LayoutOrder, Padding = UDim.new(0, 4) }),
})

local toggleRefresh = {}

local function Toggle(label, key, order)
    local row = New("TextButton", {
        Text = "",
        Size = UDim2.new(1, 0, 0, 34),
        BackgroundTransparency = 1,
        AutoButtonColor = false,
        LayoutOrder = order,
        Parent = togglesCard,
    })

    New("TextLabel", {
        Text = label,
        Font = Enum.Font.GothamMedium,
        TextSize = 13,
        TextColor3 = Theme.Text,
        BackgroundTransparency = 1,
        TextXAlignment = Enum.TextXAlignment.Left,
        Size = UDim2.new(1, -50, 1, 0),
        Parent = row,
    })

    local track = New("Frame", {
        AnchorPoint = Vector2.new(1, 0.5),
        Position = UDim2.new(1, 0, 0.5, 0),
        Size = UDim2.fromOffset(38, 22),
        BackgroundColor3 = Theme.Track,
        BorderSizePixel = 0,
        Parent = row,
    }, { New("UICorner", { CornerRadius = UDim.new(1, 0) }) })

    local thumb = New("Frame", {
        AnchorPoint = Vector2.new(0, 0.5),
        Position = UDim2.new(0, 3, 0.5, 0),
        Size = UDim2.fromOffset(16, 16),
        BackgroundColor3 = Theme.TextDim,
        BorderSizePixel = 0,
        Parent = track,
    }, { New("UICorner", { CornerRadius = UDim.new(1, 0) }) })

    local function Refresh()
        local on = config[key]
        TweenService:Create(track, TweenInfo.new(0.2, Enum.EasingStyle.Quad), {
            BackgroundColor3 = on and Theme.Accent or Theme.Track,
        }):Play()
        TweenService:Create(thumb, TweenInfo.new(0.2, Enum.EasingStyle.Quad), {
            Position = on and UDim2.new(1, -19, 0.5, 0) or UDim2.new(0, 3, 0.5, 0),
            BackgroundColor3 = on and Theme.Bg or Theme.TextDim,
        }):Play()
    end

    table.insert(toggleRefresh, Refresh)
    row.MouseButton1Click:Connect(function()
        config[key] = not config[key]
        Refresh()
    end)
    Refresh()
end

Toggle("Anti-AFK", "AntiAfk", 1)
Toggle("Hide reward popups", "HidePopups", 2)

local startBtn = New("TextButton", {
    Text = "Start Farming",
    Font = Enum.Font.GothamBold,
    TextSize = 14,
    TextColor3 = Theme.Bg,
    BackgroundColor3 = Theme.Accent,
    AutoButtonColor = false,
    BorderSizePixel = 0,
    Size = UDim2.new(1, 0, 0, 46),
    LayoutOrder = 4,
    Parent = body,
}, { New("UICorner", { CornerRadius = UDim.new(0, 12) }) })

startBtn.MouseEnter:Connect(function()
    if not Runtime.Farming then
        TweenService:Create(startBtn, TweenInfo.new(0.15), { BackgroundColor3 = Theme.AccentSoft }):Play()
    end
end)
startBtn.MouseLeave:Connect(function()
    if not Runtime.Farming then
        TweenService:Create(startBtn, TweenInfo.new(0.15), { BackgroundColor3 = Theme.Accent }):Play()
    end
end)

local autoBtn = New("TextButton", {
    Text = "Auto Farm (Server Hop)",
    Font = Enum.Font.GothamBold,
    TextSize = 12,
    TextColor3 = Theme.Accent,
    BackgroundColor3 = Theme.SurfaceAlt,
    AutoButtonColor = false,
    BorderSizePixel = 0,
    Size = UDim2.new(1, 0, 0, 36),
    LayoutOrder = 5,
    Parent = body,
}, {
    New("UICorner", { CornerRadius = UDim.new(0, 10) }),
    New("UIStroke", { Color = Theme.Accent, Thickness = 1, Transparency = 0.5 }),
})

autoBtn.MouseEnter:Connect(function()
    TweenService:Create(autoBtn, TweenInfo.new(0.15), { BackgroundColor3 = Theme.Border }):Play()
end)
autoBtn.MouseLeave:Connect(function()
    TweenService:Create(autoBtn, TweenInfo.new(0.15), { BackgroundColor3 = Theme.SurfaceAlt }):Play()
end)

RefreshUI = function()
    for _, candy in ipairs(Candy) do
        candyRefs[candy.DataName].Text = tostring(Session.Candy[candy.DataName] or 0)
    end

    local elapsed = Session.Mark and (os.time() - Session.Mark) or 0
    local sec = math.floor(elapsed)
    timeVal.Text = string.format("%02d:%02d:%02d", math.floor(sec / 3600), math.floor((sec % 3600) / 60), sec % 60)
    housesVal.Text = tostring(Session.Houses)

    local total = 0
    for _, v in pairs(Session.Candy) do total = total + v end
    totalVal.Text = tostring(total) .. " candy"

    if Runtime.Reconnecting then
        startBtn.Text = "Reconnecting..."
        startBtn.BackgroundColor3 = Theme.Danger
        startBtn.TextColor3 = Theme.Text
        statusText.Text = "reconnect"
        statusDot.BackgroundColor3 = Theme.Danger
    elseif Runtime.Farming then
        startBtn.Text = "Stop Farming"
        startBtn.BackgroundColor3 = Theme.Danger
        startBtn.TextColor3 = Theme.Text
        statusText.Text = "farming"
        statusDot.BackgroundColor3 = Theme.Success
    else
        startBtn.Text = "Start Farming"
        startBtn.BackgroundColor3 = Theme.Accent
        startBtn.TextColor3 = Theme.Bg
        statusText.Text = "idle"
        statusDot.BackgroundColor3 = Theme.TextMuted
    end

    for _, r in ipairs(toggleRefresh) do r() end
end

startBtn.MouseButton1Click:Connect(function()
    if Runtime.Reconnecting then return end
    if Runtime.Farming then StopFarm() else StartFarm() end
end)

autoBtn.MouseButton1Click:Connect(function()
    if Runtime.Reconnecting then return end
    gs.CandyFarmAutoStart = true
    gs.CandyFarmUnload()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/Fantom233/BABFT/refs/heads/main/LoopCandyFarm.lua"))()
end)

closeBtn.MouseButton1Click:Connect(function() gs.CandyFarmUnload() end)

local dragging, dragStart, dragPos = false, nil, nil
header.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging, dragStart, dragPos = true, input, main.Position
    end
end)
UserInputService.InputChanged:Connect(function(input)
    if not dragging then return end
    if input.UserInputType == Enum.UserInputType.MouseMovement or input == dragStart then
        local delta = input.Position - dragStart.Position
        main.Position = UDim2.fromOffset(dragPos.X.Offset + delta.X, dragPos.Y.Offset + delta.Y)
    end
end)
UserInputService.InputEnded:Connect(function(input)
    if dragging and (input == dragStart or input.UserInputType == Enum.UserInputType.MouseButton1) then
        dragging = false
    end
end)

local function ClampPos()
    local vp = screen.AbsoluteSize
    local sz = main.AbsoluteSize
    main.Position = UDim2.fromOffset(
        math.clamp(main.Position.X.Offset, 8, math.max(8, vp.X - sz.X - 8)),
        math.clamp(main.Position.Y.Offset, 8, math.max(8, vp.Y - sz.Y - 8))
    )
end

local function FitScale()
    local vp = screen.AbsoluteSize
    if vp.X < 1 or vp.Y < 1 then return end
    local cur = scale.Scale > 0 and scale.Scale or 1
    local unscaled = main.AbsoluteSize / cur
    scale.Scale = math.clamp(math.min(1, (vp.X - 16) / unscaled.X, (vp.Y - 16) / math.max(unscaled.Y, 1)), 0.5, 1)
    ClampPos()
end

local minimized = false
minBtn.MouseButton1Click:Connect(function()
    minimized = not minimized
    body.Visible = not minimized
    FitScale()
end)

main.Position = UDim2.fromOffset(20, math.max(20, (viewport.Y - 400) / 2))
if minimized then body.Visible = false end
RefreshUI()
FitScale()

screen:GetPropertyChangedSignal("AbsoluteSize"):Connect(FitScale)
main:GetPropertyChangedSignal("AbsoluteSize"):Connect(ClampPos)

TweenService:Create(main, TweenInfo.new(0.4, Enum.EasingStyle.Quint), { BackgroundTransparency = 0 }):Play()

task.spawn(function()
    while Runtime.Running do
        task.wait(1)
        if Runtime.Farming and RefreshUI then RefreshUI() end
        if config.HidePopups then HidePopup() end
    end
end)

gs.CandyFarmUnload = function()
    if not Runtime.Running then return end
    Runtime.Running = false
    Runtime.Farming = false
    screen:Destroy()
    if hiddenPopup then hiddenPopup.Disabled = false end
    gs.CandyFarmUnload = nil
end
