
local function getnamecall() -- u can add placeid detector with all namecalls & remotes if we want later on
    return "UpdateMousePos1"
end
 
 local namecalltype = getnamecall()
 
local function MainEventLocate()
    for _,v in pairs(game:GetService("ReplicatedStorage"):GetDescendants()) do
        if v.Name == "MainEvent" then
            return v
        end
    end
 end
 
 local mainevent = MainEventLocate()
 
 -- // Shorthand
 local uwuGult = getgenv().Gult
 local uwuMain = uwuGult.Options
 local uwuAimAssistMain = uwuGult.AimAssist.Main
 local uwuAimAssistFOV = uwuGult.AimAssist.FOV
 local uwuSilentAimMain = uwuGult.SilentAim.Main
 local uwuAntiGroundShots = uwuGult.SilentAim.AntiGroundShots
 local uwuAntiCurve = uwuGult.SilentAim.AntiCurve
 local uwuSilentAimFOV = uwuGult.SilentAim.FOV
 local uwuTrace = uwuGult.Snapline
 local uwuPingPred = uwuGult.PingPrediction
 local uwuFAG = uwuGult.WaterMark
 local uwuBLACKDICK = uwuGult.Visuals.DistanceESP
 local uwuHAHAHAHAH = uwuGult.Visuals.WeaponESP
 local uwuNIGGER = uwuGult.CFrame
 local uwuCUMCUMCUM = uwuGult.Extra.TrashTalk
 local uwuNIGGA = uwuGult.Visuals.HealthBar
 local uwuPENIS = uwuGult.Visuals.NameESP
 local uwuAHAAHAAHHAHAHA = uwuGult.Visuals.Radar
 local uwuAUFHAUYFGHYUFHFUHJ = uwuGult.Desync
 

 
 -- // Optimization
 local vect3 = Vector3.new
 local vect2 = Vector2.new
 local cnew = CFrame.new
 
 -- // Libraries
 local NotificationHolder = loadstring(game:HttpGet("https://raw.githubusercontent.com/BocusLuke/UI/main/STX/Module.Lua"))()
 local Notification = loadstring(game:HttpGet("https://raw.githubusercontent.com/cloudtad9/daasddadsadadsad/main/adadassadasd"))()
 local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Consistt/Ui/main/UnLeaked"))()
 
 -- // Services
 local uis = game:GetService("UserInputService")
 local rs = game:GetService("RunService")
 local plrs = game:GetService("Players")
 local ws = game:GetService("Workspace")
 
 -- // Script Variables
 local CToggle = false
 local lplr = plrs.LocalPlayer
 local CTarget = nil
 local CPart = nil
 local SToggle = false
 local STarget = nil
 local SPart = nil
 
 -- // Client Variables
 local m = lplr:GetMouse()
 local c = ws.CurrentCamera
 
 local function SendNotification(text)
    Notification:Notify(
        {Title = "Gult - 战利品乐趣", Description = " "..text},
        {OutlineColor = Color3.fromRGB(255,255,255),Time = 2, Type = "image"},
        {Image = "http://www.roblox.com/asset/?id=6023426923", ImageColor = Color3.fromRGB(255,255,255)}
    )
 end 
 
 -- // Call notification function
 if uwuMain.Notifications then
    SendNotification("injecting Gult")
    wait(3.5)
    SendNotification("Gult.fun")
    wait(3.5)
    SendNotification("Start 2 tapping")
 end
 
 -- // Camlock FOV
 local AimAssistFOV = Drawing.new("Circle")
 AimAssistFOV.Visible = uwuAimAssistFOV.ShowFOV
 AimAssistFOV.Thickness = 1
 AimAssistFOV.NumSides = 30
 AimAssistFOV.Radius = uwuAimAssistFOV.Radius * 3
 AimAssistFOV.Color = uwuAimAssistFOV.Color
 AimAssistFOV.Filled = uwuAimAssistFOV.Filled
 AimAssistFOV.Transparency = uwuAimAssistFOV.Transparency
 
 --Silent FOV
 local SilentAimFOV = Drawing.new("Circle")
 SilentAimFOV.Visible = uwuSilentAimFOV.ShowFOV
 SilentAimFOV.Thickness = 1
 SilentAimFOV.NumSides = 30
 SilentAimFOV.Radius = uwuSilentAimFOV.Radius * 3
 SilentAimFOV.Color = uwuSilentAimFOV.Color
 SilentAimFOV.Filled = uwuSilentAimFOV.Filled
 SilentAimFOV.Transparency = uwuSilentAimFOV.Transparency
 
 --Tracer
 local Line = Drawing.new("Line")
 Line.Color = uwuTrace.Color
 Line.Transparency = uwuTrace.Transparency
 Line.Thickness = 1
 Line.Visible = uwuTrace.Visible
 
 -- // Script Functions
 local function uwuFindTawget() -- // Find target
    local d, t = math.huge, nil
    for _,v in pairs (plrs:GetPlayers()) do
        local _,os = c:WorldToViewportPoint(v.Character.PrimaryPart.Position)
        if v ~= lplr and v.Character and v.Character:FindFirstChild("Humanoid") and v.Character.Humanoid.Health ~= 0 and v.Character:FindFirstChild("HumanoidRootPart") and os then
            local pos = c:WorldToViewportPoint(v.Character.PrimaryPart.Position)
            local magnitude = (vect2(pos.X, pos.Y) - vect2(m.X, m.Y + 36)).magnitude
            if magnitude < d then
                t = v
                d = magnitude
            end
        end
    end
    return t
 end
 
 local function uwuFindPart() -- // Find aimpart
    local d, p = math.huge, nil
    if CTarget then
        for _,v in pairs(CTarget.Character:GetChildren()) do
            if table.find(uwuAimAssistMain.Parts, v.Name) then
                local pos = c:WorldToViewportPoint(v.Position)
                local Magn = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
                if Magn < d then
                    d = Magn
                    p = v
                end
            end
        end
        return p.Name
    end
 end
 
 local function uwuFindSilentPart() -- // Find aimpart
    local d, p = math.huge, nil
    if CTarget then
        for _,v in pairs(CTarget.Character:GetChildren()) do
            if table.find(uwuSilentAimMain.Parts, v.Name) then
                local pos = c:WorldToViewportPoint(v.Position)
                local Magn = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
                if Magn < d then
                    d = Magn
                    p = v
                end
            end
        end
        return p.Name
    end
 end
 
 local function uwuCheckAnti(targ) -- // Anti-aim detection
    if (targ.Character.HumanoidRootPart.Velocity.Y < -5 and targ.Character.Humanoid:GetState() ~= Enum.HumanoidStateType.Freefall) or targ.Character.HumanoidRootPart.Velocity.Y < -50 then
        return true
    elseif targ and (targ.Character.HumanoidRootPart.Velocity.X > 35 or targ.Character.HumanoidRootPart.Velocity.X < -35) then
        return true
    elseif targ and targ.Character.HumanoidRootPart.Velocity.Y > 60 then
        return true
    elseif targ and (targ.Character.HumanoidRootPart.Velocity.Z > 35 or targ.Character.HumanoidRootPart.Velocity.Z < -35) then
        return true
    else
        return false
    end
 end
 
 local function InSilentRadiuwus(target, section, fov) -- // Check if player is in the fov
    if target then
        local pos = nil
        if not uwuCheckAnti(target) then
            pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + target.Character.PrimaryPart.Velocity * section.Prediction)
        else
            pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + ((target.Character.Humanoid.MoveDirection * target.Character.Humanoid.WalkSpeed) * section.Prediction))
        end
        local mag = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
        if mag < fov * 3 then
            return true
        else
            return false
        end
    end
 end
 
 local function Silent()
    if STarget then
        if SPart and InSilentRadiuwus(STarget, uwuSilentAimMain, SilentAimFOV.Radius) then
            if not uwuCheckAnti(STarget) then
                mainevent:FireServer(namecalltype, STarget.Character[SPart].Position + (STarget.Character[SPart].Velocity * uwuSilentAimMain.Prediction))
            else
                mainevent:FireServer(namecalltype, STarget.Character[SPart].Position + ((STarget.Character.Humanoid.MoveDirection * STarget.Character.Humanoid.WalkSpeed) * uwuSilentAimMain.Prediction))
            end
        end
    end
 end
 
 
 local function InRadiuwus(target, section, fov) -- // Check if player is in the fov
    if target then
        if uwuAimAssistFOV.UseFOV then
            local pos = nil
            if not uwuCheckAnti(target) then
                pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + target.Character.PrimaryPart.Velocity * section.Prediction)
            else
                pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + ((target.Character.Humanoid.MoveDirection * target.Character.Humanoid.WalkSpeed) * section.Prediction))
            end
            local mag = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
            if mag < fov * 3 then
                return true
            else
                return false
            end
        else
            return true
        end
    end
 end
 
 uis.InputBegan:Connect(function(k,t)
    if not t then
        if k.KeyCode == Enum.KeyCode[uwuAimAssistMain.Key:upper()] then
            if CTarget == nil then
            CToggle = true
            CTarget = uwuFindTawget()
            if uwuMain.Notifications then
                SendNotification("Aim Target "..CTarget.Name)
            end
       else
            if CToggle == true then
                CToggle = false
                CTarget = nil
                if uwuMain.Notifications then
                    SendNotification("Unlocked")
                end
            end
        end
        elseif k.KeyCode == Enum.KeyCode[uwuSilentAimMain.KeyBind:upper()] and uwuSilentAimMain.Mode == "Regular" then
            if SToggle then
                SToggle = false
                if uwuMain.Notifications then
                    SendNotification("silent disabled")
                end
            else
                SToggle = true
                if uwuMain.Notifications then
                    SendNotification("silent enabled")
                end
            end
        end
    end
end)
 
 rs.RenderStepped:Connect(function()
    if CTarget then
        CPart = uwuFindPart()
        local pos = nil
        local cum = nil
        if CTarget.Character.BodyEffects["K.O"].Value == true or lplr.Character.BodyEffects["K.O"].Value == true then
            CToggle = false
            CTarget = nil
        else
            if uwuAimAssistMain.Shake then
                if uwuAimAssistMain.PredictMovement then
                    if not uwuCheckAnti(CTarget) then
                        cum = CTarget.Character[CPart].Position + CTarget.Character[CPart].Velocity * uwuAimAssistMain.Prediction + (vect3(
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue)
                        ) * 0.1)
                    else
                        cum = CTarget.Character[CPart].Position + ((CTarget.Character.Humanoid.MoveDirection * CTarget.Character.Humanoid.WalkSpeed) * uwuAimAssistMain.Prediction + (vect3(
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue)
                        ) * 0.1))
                    end
                    pos = c:WorldToViewportPoint(cum)
                else
                    cum = CTarget.Character[CPart].Position + (vect3(
                        math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                        math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                        math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue)
                    ) * 0.1)
                    pos = c:WorldToViewportPoint(cum)
                end
            else
                if uwuAimAssistMain.PredictMovement then
                    if not uwuCheckAnti(CTarget) then
                        cum = CTarget.Character[CPart].Position + CTarget.Character[CPart].Velocity * uwuAimAssistMain.Prediction
                    else
                        cum = CTarget.Character[CPart].Position + ((CTarget.Character.Humanoid.MoveDirection * CTarget.Character.Humanoid.WalkSpeed) * uwuAimAssistMain.Prediction)
                    end
                    pos = c:WorldToViewportPoint(cum)
                else
                    cum = CTarget.Character[CPart].Position
                    pos = c:WorldToViewportPoint(cum)
                end
            end
            if InRadiuwus(CTarget, uwuAimAssistMain, AimAssistFOV.Radius) then
                local main = nil
                if uwuAimAssistMain.SmoothLock then
                    main = cnew(c.CFrame.p, cum)
                    c.CFrame = c.CFrame:Lerp(main, uwuAimAssistMain.Smoothness, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)
                else
                    c.CFrame = cnew(c.CFrame.p, cum)
                end
            end
            if uwuMain.FOVMode == "FollowMouse" then
                if uwuAimAssistFOV.ShowFOV then
                    AimAssistFOV.Position = vect2(m.X, m.Y + 36)
                end
                if uwuSilentAimFOV.ShowFOV then
                    SilentAimFOV.Position = vect2(m.X, m.Y + 36)
                end
            elseif uwuMain.FOVMode == "Sticky" then
                if uwuAimAssistFOV.ShowFOV then
                    AimAssistFOV.Position = vect2(pos.X, pos.Y)
                end
                if uwuSilentAimFOV.ShowFOV then
                    SilentAimFOV.Position = vect2(pos.X, pos.Y)
                end
            end
            if uwuTrace.Enabled then
                Line.Visible = true
                Line.From = vect2(m.X, m.Y + 36)
                Line.To = vect2(pos.X, pos.Y)
            end
        end
    else
        AimAssistFOV.Position = vect2(m.X, m.Y + 36)
        SilentAimFOV.Position = vect2(m.X, m.Y + 36)
        Line.Visible = false
    end
 end)
 
 lplr.Character.ChildAdded:Connect(function(tool)
    if tool:IsA("Tool") then
        tool.Activated:connect(function()
            if uwuSilentAimMain.Mode == "Regular" then
                if SToggle then
                    STarget = uwuFindTawget()
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            elseif uwuSilentAimMain.Mode == "Target" then
                if CToggle then
                    STarget = CTarget
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            end
        end)
    end
 end)
 
 lplr.CharacterAdded:Connect(function(char)
    char.ChildAdded:Connect(function(tool)
        tool.Activated:connect(function()
            if uwuSilentAimMain.Mode == "Regular" then
                if SToggle then
                    STarget = uwuFindTawget()
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            elseif uwuSilentAimMain.Mode == "Target" then
                if CToggle then
                    STarget = CTarget
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            end
        end)
    end)
 end)
 
 --Ping Prediction
 coroutine.resume(coroutine.create(function()
    while true do
        if uwuPingPred.Enabled then
            local ping = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValue()
            if ping <= 40 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping30_40
            elseif ping <= 50 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping40_50
            elseif ping <= 60 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping50_60
            elseif ping <= 70 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping60_70
            elseif ping <= 80 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping70_80
            elseif ping <= 90 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping80_90
            elseif ping <= 100 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping90_100
            elseif ping <= 110 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping100_110
            elseif ping <= 120 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping110_120
            elseif ping <= 130 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping120_130
            elseif ping <= 140 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping130_140
            elseif ping <= 150 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping140_150
            elseif ping <= 160 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping150_160
            elseif ping <= 170 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping160_170
            elseif ping <= 180 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping170_180
            elseif ping <= 190 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping180_190
            elseif ping <= 200 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping190_200
            end
            task.wait(0.7)
        end
    end
 end))

--// DistanceESP \\--
 if uwuBLACKDICK == true then
    local c = workspace.CurrentCamera
    local ps = game:GetService("Players")
    local lp = ps.LocalPlayer
    local rs = game:GetService("RunService")
    
    local function getdistancefc(part)
        return (part.Position - c.CFrame.Position).Magnitude
    end
    
    local function esp(p,cr)
        local h = cr:WaitForChild("Humanoid")
        local hrp = cr:WaitForChild("LeftLowerLeg")
    
        local text = Drawing.new("Text")
        text.Visible = false
        text.Center = true 
        text.Outline = true 
        text.Font = 2
        text.Color = Color3.fromRGB(255,255,255)
        text.Size = 13
    
        local c1 
        local c2 
        local c3 
    
        local function dc()
            text.Visible = false
            text:Remove()
            if c1 then
                c1:Disconnect()
                c1 = nil 
            end
            if c2 then
                c2:Disconnect()
                c2 = nil 
            end
            if c3 then
                c3:Disconnect()
                c3 = nil 
            end
        end
    
        c2 = cr.AncestryChanged:Connect(function(_,parent)
            if not parent then
                dc()
            end
        end)
    
        c3 = h.HealthChanged:Connect(function(v)
            if (v<=0) or (h:GetState() == Enum.HumanoidStateType.Dead) then
                dc()
            end
        end)
    
        c1 = rs.RenderStepped:Connect(function()
            local hrp_pos,hrp_os = c:WorldToViewportPoint(hrp.Position)
            if hrp_os then
                text.Position = Vector2.new(hrp_pos.X,hrp_pos.Y)
                text.Text = '['..tostring(math.floor(getdistancefc(hrp)))..'m]'
                text.Visible = true 
            else
                text.Visible = false 
            end
        end)
    end
    
    local function p_added(p)
        if p.Character then
            esp(p,p.Character)
        end
        p.CharacterAdded:Connect(function(cr)
            esp(p,cr)
        end)
    end
    
    
    for i,p in next, ps:GetPlayers() do 
        if p ~= lp then
            p_added(p)
        end
    end
    
    ps.PlayerAdded:Connect(p_added)
     end
--// WeaponESP \\--
if uwuHAHAHAHAH == true then
    local c = workspace.CurrentCamera
local ps = game:GetService("Players")
local lp = ps.LocalPlayer
local rs = game:GetService("RunService")

local function ftool(cr)
    for a,b in next, cr:GetChildren() do 
        if b.ClassName == 'Tool' then
            return tostring(b.Name)
        end
    end
    return 'empty'
end

local function esp(p,cr)
    local h = cr:WaitForChild("Humanoid")
    local hrp = cr:WaitForChild("HumanoidRootPart")

    local text = Drawing.new('Text')
    text.Visible = false
    text.Center = true
    text.Outline = true
    text.Color = Color3.new(1,1,1)
    text.Font = 2
    text.Size = 13

    local c1 
    local c2
    local c3 

    local function dc()
        text.Visible = false
        text:Remove()
        if c3 then
            c1:Disconnect()
            c2:Disconnect()
            c3:Disconnect()
            c1 = nil 
            c2 = nil
            c3 = nil
        end
    end

    c2 = cr.AncestryChanged:Connect(function(_,parent)
        if not parent then
            dc()
        end
    end)

    c3 = h.HealthChanged:Connect(function(v)
        if (v<=0) or (h:GetState() == Enum.HumanoidStateType.Dead) then
            dc()
        end
    end)

    c1 = rs.Heartbeat:Connect(function()
        local hrp_pos,hrp_os = c:WorldToViewportPoint(hrp.Position)
        if hrp_os then
            text.Position = Vector2.new(hrp_pos.X, hrp_pos.Y)
            text.Text = ' '..tostring(ftool(cr))..' '
            text.Visible = true
        else
            text.Visible = false
        end
    end)

end

local function p_added(p)
    if p.Character then
        esp(p,p.Character)
    end
    p.CharacterAdded:Connect(function(cr)
        esp(p,cr)
    end)
end

for a,b in next, ps:GetPlayers() do 
    if b ~= lp then
        p_added(b)
    end
end

ps.PlayerAdded:Connect(p_added)
end

--// WaterMark \\--
if uwuFAG.Enabled then

library.rank = "Gult free build"
local Wm = library:Watermark("Gult.fun | v" .. library.version ..  " | " .. library:GetUsername() .. " | rank: " .. library.rank)
if getgenv().Gult.WaterMark.ShowFPS == true then
    local FpsWm = Wm:AddWatermark("fps: " .. library.fps)
coroutine.wrap(function()
    while wait(.75) do
        FpsWm:Text("fps: " .. library.fps)
    end
end)()
end
end

--// CFrame \\--
if uwuNIGGER.Enabled then
    repeat
        wait()
    until game:IsLoaded()
    local L_134_ = game:service('Players')
    local L_135_ = L_134_.LocalPlayer
    repeat
        wait()
    until L_135_.Character
    local L_136_ = game:service('UserInputService')
    local L_137_ = game:service('RunService')
    getgenv().Multiplier = 0.5
    local L_138_ = true
    local L_139_
    L_136_.InputBegan:connect(function(L_140_arg0)
        if L_140_arg0.KeyCode == Enum.KeyCode.LeftBracket then
            Multiplier = Multiplier + 0.01
            print(Multiplier)
            wait(0.2)
            while L_136_:IsKeyDown(Enum.KeyCode.LeftBracket) do
                wait()
                Multiplier = Multiplier + 0.01
                print(Multiplier)
            end
        end
        if L_140_arg0.KeyCode == Enum.KeyCode.RightBracket then
            Multiplier = Multiplier - 0.01
            print(Multiplier)
            wait(0.2)
            while L_136_:IsKeyDown(Enum.KeyCode.RightBracket) do
                wait()
                Multiplier = Multiplier - 0.01
                print(Multiplier)
            end
        end
        if L_140_arg0.KeyCode == Enum.KeyCode[uwuNIGGER.Toggle:upper()] then
            L_138_ = not L_138_
            if L_138_ == true then
                repeat
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + game.Players.LocalPlayer.Character.Humanoid.MoveDirection * Multiplier
                    game:GetService("RunService").Stepped:wait()
                until L_138_ == false
            end
        end
    end)
end

--// TrashTalk \\--
if uwuCUMCUMCUM == true then
    local words = {
        'GULT FREE RUNS YOU',
        'quit missing ur shots and tapn GULT',
        'lolol BAND4BAND DEMONS LOFI N VIKO',
        'gulp wt r u gna do',
        'come tap with a real script 😭🙏',
        
    }
    
    local player = game.Players.LocalPlayer
    local keybind = 'y'
    
    local event = game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest
    
    player:GetMouse().KeyDown:connect(function(key)
        if key == keybind then
            event:FireServer(words[math.random(#words)], "All")
        end
    end)
end

--// Box & Health ESP \\--
if uwuNIGGA == true then

local Settings = {
    Box_Color = Color3.fromRGB(255, 0, 0),
    Box_Thickness = 0.1,
}

local Team_Check = {
    TeamCheck = false, -- if TeamColor is on this won't matter...
    Green = Color3.fromRGB(0, 255, 0),
    Red = Color3.fromRGB(255, 0, 0)
}
local TeamColor = true

--// SEPARATION
local player = game:GetService("Players").LocalPlayer
local camera = game:GetService("Workspace").CurrentCamera
local mouse = player:GetMouse()

local function NewQuad(thickness, color)
    local quad = Drawing.new("Quad")
    quad.Visible = false
    quad.PointA = Vector2.new(0,0)
    quad.PointB = Vector2.new(0,0)
    quad.PointC = Vector2.new(0,0)
    quad.PointD = Vector2.new(0,0)
    quad.Color = color
    quad.Filled = false
    quad.Thickness = thickness
    quad.Transparency = 1
    return quad
end

local function NewLine(thickness, color)
    local line = Drawing.new("Line")
    line.Visible = false
    line.From = Vector2.new(0, 0)
    line.To = Vector2.new(0, 0)
    line.Color = color 
    line.Thickness = thickness
    line.Transparency = 1
    return line
end

local function Visibility(state, lib)
    for u, x in pairs(lib) do
        x.Visible = state
    end
end

local function ToColor3(col) --Function to convert, just cuz c;
    local r = col.r --Red value
    local g = col.g --Green value
    local b = col.b --Blue value
    return Color3.new(r,g,b); --Color3 datatype, made of the RGB inputs
end

local black = Color3.fromRGB(0, 0 ,0)
local function ESP(plr)
    local library = {
        --//Box and Black Box(black border)
        black = NewQuad(Settings.Box_Thickness*2, black),
        box = NewQuad(Settings.Box_Thickness, Settings.Box_Color),
        --//Bar and Green Health Bar (part that moves up/down)
        healthbar = NewLine(3, black),
        greenhealth = NewLine(1.5, black)
    }

    local function Colorize(color)
        for u, x in pairs(library) do
            if x ~= library.healthbar and x ~= library.greenhealth then
                x.Color = color
            end
        end
    end

    local function Updater()
        local connection
        connection = game:GetService("RunService").RenderStepped:Connect(function()
            if plr.Character ~= nil and plr.Character:FindFirstChild("Humanoid") ~= nil and plr.Character:FindFirstChild("HumanoidRootPart") ~= nil and plr.Character.Humanoid.Health > 0 and plr.Character:FindFirstChild("Head") ~= nil then
                local HumPos, OnScreen = camera:WorldToViewportPoint(plr.Character.HumanoidRootPart.Position)
                if OnScreen then
                    local head = camera:WorldToViewportPoint(plr.Character.Head.Position)
                    local DistanceY = math.clamp((Vector2.new(head.X, head.Y) - Vector2.new(HumPos.X, HumPos.Y)).magnitude, 2, math.huge)
                    
                    local function Size(item)
                        item.PointA = Vector2.new(HumPos.X + DistanceY, HumPos.Y - DistanceY*2)
                        item.PointB = Vector2.new(HumPos.X - DistanceY, HumPos.Y - DistanceY*2)
                        item.PointC = Vector2.new(HumPos.X - DistanceY, HumPos.Y + DistanceY*2)
                        item.PointD = Vector2.new(HumPos.X + DistanceY, HumPos.Y + DistanceY*2)
                    end
                    Size(library.box)
                    Size(library.black)


                    --// Health Bar
                    local d = (Vector2.new(HumPos.X - DistanceY, HumPos.Y - DistanceY*2) - Vector2.new(HumPos.X - DistanceY, HumPos.Y + DistanceY*2)).magnitude 
                    local healthoffset = plr.Character.Humanoid.Health/plr.Character.Humanoid.MaxHealth * d

                    library.greenhealth.From = Vector2.new(HumPos.X - DistanceY - 4, HumPos.Y + DistanceY*2)
                    library.greenhealth.To = Vector2.new(HumPos.X - DistanceY - 4, HumPos.Y + DistanceY*2 - healthoffset)

                    library.healthbar.From = Vector2.new(HumPos.X - DistanceY - 4, HumPos.Y + DistanceY*2)
                    library.healthbar.To = Vector2.new(HumPos.X - DistanceY - 4, HumPos.Y - DistanceY*2)

                    local green = Color3.fromRGB(0, 255, 0)
                    local red = Color3.fromRGB(255, 0, 0)

                    library.greenhealth.Color = red:lerp(green, plr.Character.Humanoid.Health/plr.Character.Humanoid.MaxHealth);

                    if Team_Check.TeamCheck then
                        if plr.TeamColor == player.TeamColor then
                            Colorize(Team_Check.Green)
                        else 
                            Colorize(Team_Check.Red)
                        end
                    else 
                        
                    end
                    if TeamColor == true then
                        Colorize(plr.TeamColor.Color)
                    end
                    Visibility(true, library)
                else 
                    Visibility(false, library)
                end
            else 
                Visibility(false, library)
                if game.Players:FindFirstChild(plr.Name) == nil then
                    connection:Disconnect()
                end
            end
        end)
    end
    coroutine.wrap(Updater)()
end

for i, v in pairs(game:GetService("Players"):GetPlayers()) do
    if v.Name ~= player.Name then
        coroutine.wrap(ESP)(v)
    end
end

game.Players.PlayerAdded:Connect(function(newplr)
    if newplr.Name ~= player.Name then
        coroutine.wrap(ESP)(newplr)
    end
end)
end

--// NameESP \\--
if uwuPENIS == true then
    local c = workspace.CurrentCamera
local ps = game:GetService("Players")
local lp = ps.LocalPlayer
local rs = game:GetService("RunService")

local function esp(p,cr)
    local h = cr:WaitForChild("Humanoid")
    local hrp = cr:WaitForChild("Head")

    local text = Drawing.new("Text")
    text.Visible = false
    text.Center = true
    text.Outline = true 
    text.Font = 2
    text.Color = Color3.fromRGB(255,255,255)
    text.Size = 13

    local c1
    local c2
    local c3

    local function dc()
        text.Visible = false
        text:Remove()
        if c1 then
            c1:Disconnect()
            c1 = nil 
        end
        if c2 then
            c2:Disconnect()
            c2 = nil 
        end
        if c3 then
            c3:Disconnect()
            c3 = nil 
        end
    end

    c2 = cr.AncestryChanged:Connect(function(_,parent)
        if not parent then
            dc()
        end
    end)

    c3 = h.HealthChanged:Connect(function(v)
        if (v<=0) or (h:GetState() == Enum.HumanoidStateType.Dead) then
            dc()
        end
    end)

    c1 = rs.RenderStepped:Connect(function()
        local hrp_pos,hrp_onscreen = c:WorldToViewportPoint(hrp.Position)
        if hrp_onscreen then
            text.Position = Vector2.new(hrp_pos.X, hrp_pos.Y)
            text.Text = p.Name
            text.Visible = true
        else
            text.Visible = false
        end
    end)
end

local function p_added(p)
    if p.Character then
        esp(p,p.Character)
    end
    p.CharacterAdded:Connect(function(cr)
        esp(p,cr)
    end)
end

for i,p in next, ps:GetPlayers() do 
    if p ~= lp then
        p_added(p)
    end
end

ps.PlayerAdded:Connect(p_added)
end

if uwuAHAAHAAHHAHAHA == true then
    local Players = game:service("Players")
local Player = Players.LocalPlayer
local Mouse = Player:GetMouse()
local Camera = game:service("Workspace").CurrentCamera
local RS = game:service("RunService")
local UIS = game:service("UserInputService")

repeat wait() until Player.Character ~= nil and Player.Character.PrimaryPart ~= nil

local LerpColorModule = loadstring(game:HttpGet("https://pastebin.com/raw/QsnfmCpj"))()
local HealthBarLerp = LerpColorModule:Lerp(Color3.fromRGB(255, 0, 0), Color3.fromRGB(0, 255, 0))

local function NewCircle(Transparency, Color, Radius, Filled, Thickness)
    local c = Drawing.new("Circle")
    c.Transparency = Transparency
    c.Color = Color
    c.Visible = false
    c.Thickness = Thickness
    c.Position = Vector2.new(0, 0)
    c.Radius = Radius
    c.NumSides = math.clamp(Radius*55/100, 10, 75)
    c.Filled = Filled

    return c
end

local RadarInfo = {
    Position = Vector2.new(200, 200),
    Radius = 100,
    Scale = 1, -- Determinant factor on the effect of the relative position for the 2D integration
    RadarBack = Color3.fromRGB(10, 10, 10),
    RadarBorder = Color3.fromRGB(75, 75, 75),
    LocalPlayerDot = Color3.fromRGB(255, 255, 255),
    PlayerDot = Color3.fromRGB(60, 170, 255),
    Team = Color3.fromRGB(0, 255, 0),
    Enemy = Color3.fromRGB(255, 0, 0),
    Health_Color = true,
    Team_Check = true
}

local RadarBackground = NewCircle(0.9, RadarInfo.RadarBack, RadarInfo.Radius, true, 1)
RadarBackground.Visible = true
RadarBackground.Position = RadarInfo.Position

local RadarBorder = NewCircle(0.75, RadarInfo.RadarBorder, RadarInfo.Radius, false, 3)
RadarBorder.Visible = true
RadarBorder.Position = RadarInfo.Position

local function GetRelative(pos)
    local char = Player.Character
    if char ~= nil and char.PrimaryPart ~= nil then
        local pmpart = char.PrimaryPart
        local camerapos = Vector3.new(Camera.CFrame.Position.X, pmpart.Position.Y, Camera.CFrame.Position.Z)
        local newcf = CFrame.new(pmpart.Position, camerapos)
        local r = newcf:PointToObjectSpace(pos)
        return r.X, r.Z
    else
        return 0, 0
    end
end

local function PlaceDot(plr)
    local PlayerDot = NewCircle(1, RadarInfo.PlayerDot, 3, true, 1)

    local function Update()
        local c 
        c = game:service("RunService").RenderStepped:Connect(function()
            local char = plr.Character
            if char and char:FindFirstChildOfClass("Humanoid") and char.PrimaryPart ~= nil and char:FindFirstChildOfClass("Humanoid").Health > 0 then
                local hum = char:FindFirstChildOfClass("Humanoid")
                local scale = RadarInfo.Scale
                local relx, rely = GetRelative(char.PrimaryPart.Position)
                local newpos = RadarInfo.Position - Vector2.new(relx * scale, rely * scale) 
                
                if (newpos - RadarInfo.Position).magnitude < RadarInfo.Radius-2 then 
                    PlayerDot.Radius = 3   
                    PlayerDot.Position = newpos
                    PlayerDot.Visible = true
                else 
                    local dist = (RadarInfo.Position - newpos).magnitude
                    local calc = (RadarInfo.Position - newpos).unit * (dist - RadarInfo.Radius)
                    local inside = Vector2.new(newpos.X + calc.X, newpos.Y + calc.Y)
                    PlayerDot.Radius = 2
                    PlayerDot.Position = inside
                    PlayerDot.Visible = true
                end

                PlayerDot.Color = RadarInfo.PlayerDot
                if RadarInfo.Team_Check then
                    if plr.TeamColor == Player.TeamColor then
                        PlayerDot.Color = RadarInfo.Team
                    else
                        PlayerDot.Color = RadarInfo.Enemy
                    end
                end

                if RadarInfo.Health_Color then
                    PlayerDot.Color = HealthBarLerp(hum.Health / hum.MaxHealth)
                end
            else 
                PlayerDot.Visible = false
                if Players:FindFirstChild(plr.Name) == nil then
                    PlayerDot:Remove()
                    c:Disconnect()
                end
            end
        end)
    end
    coroutine.wrap(Update)()
end

for _,v in pairs(Players:GetChildren()) do
    if v.Name ~= Player.Name then
        PlaceDot(v)
    end
end

local function NewLocalDot()
    local d = Drawing.new("Triangle")
    d.Visible = true
    d.Thickness = 1
    d.Filled = true
    d.Color = RadarInfo.LocalPlayerDot
    d.PointA = RadarInfo.Position + Vector2.new(0, -6)
    d.PointB = RadarInfo.Position + Vector2.new(-3, 6)
    d.PointC = RadarInfo.Position + Vector2.new(3, 6)
    return d
end

local LocalPlayerDot = NewLocalDot()

Players.PlayerAdded:Connect(function(v)
    if v.Name ~= Player.Name then
        PlaceDot(v)
    end
    LocalPlayerDot:Remove()
    LocalPlayerDot = NewLocalDot()
end)

-- Loop
coroutine.wrap(function()
    local c 
    c = game:service("RunService").RenderStepped:Connect(function()
        if LocalPlayerDot ~= nil then
            LocalPlayerDot.Color = RadarInfo.LocalPlayerDot
            LocalPlayerDot.PointA = RadarInfo.Position + Vector2.new(0, -6)
            LocalPlayerDot.PointB = RadarInfo.Position + Vector2.new(-3, 6)
            LocalPlayerDot.PointC = RadarInfo.Position + Vector2.new(3, 6)
        end
        RadarBackground.Position = RadarInfo.Position
        RadarBackground.Radius = RadarInfo.Radius
        RadarBackground.Color = RadarInfo.RadarBack

        RadarBorder.Position = RadarInfo.Position
        RadarBorder.Radius = RadarInfo.Radius
        RadarBorder.Color = RadarInfo.RadarBorder
    end)
end)()

-- Draggable
local inset = game:service("GuiService"):GetGuiInset()

local dragging = false
local offset = Vector2.new(0, 0)
UIS.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 and (Vector2.new(Mouse.X, Mouse.Y + inset.Y) - RadarInfo.Position).magnitude < RadarInfo.Radius then
        offset = RadarInfo.Position - Vector2.new(Mouse.X, Mouse.Y)
        dragging = true
    end
end)

UIS.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = false
    end
end)

coroutine.wrap(function()
    local dot = NewCircle(1, Color3.fromRGB(255, 255, 255), 3, true, 1)
    local c 
    c = game:service("RunService").RenderStepped:Connect(function()
        if (Vector2.new(Mouse.X, Mouse.Y + inset.Y) - RadarInfo.Position).magnitude < RadarInfo.Radius then
            dot.Position = Vector2.new(Mouse.X, Mouse.Y + inset.Y)
            dot.Visible = true
        else 
            dot.Visible = false
        end
        if dragging then
            RadarInfo.Position = Vector2.new(Mouse.X, Mouse.Y) + offset
        end
    end)
end)()

--[[ Example:
wait(3)
RadarInfo.Position = Vector2.new(300, 300)
RadarInfo.Radius = 150
RadarInfo.RadarBack = Color3.fromRGB(50, 0, 0)
]]

-- // anti ground shots
if uwuAntiGroundShots == true then
    if Target.Character.HumanoidRootPart.Velocity.Y < -20 then
        pcall(function()
            local Part = Target.Character.HumanoidRootPart
            Part.Velocity = Vector3.new(Part.Velocity.X, 0, Part.Velocity.Z)
            Part.AssemblyLinearVelocity = Vector3.new(Part.Velocity.X, 0, Part.Velocity.Z)
        end)
    end
    end

-- // Desync \\ --
if uwuAUFHAUYFGHYUFHFUHJ.Enabled then
    

local settings = getgenv().Gult.Desync

--[[
┏━┓┏━━┓┏┓
┃┃┃┣━━┃┃┃
┃┃┃┃━━┫┃┗┓
┗━┛┗━━┛┗━┛

Left , Right , One , Zero , Behind , Forward 
]]--
loadstring(game:HttpGet("https://pastebin.com/raw/qCdp9Bfi"))()
end

-- // anti curve

function AntiCurve()
    local character = game.Players.LocalPlayer.Character
    if getgenv().Gult.SilentAim.Anti_Curve and character and character.PrimaryPart then
        local characterCf = character.PrimaryPart.CFrame
        local target = self.Character.HumanoidRootPart
        local targetPos = target.Position
        local charPos = character.PrimaryPart.Position
        character:SetPrimaryPartCFrame(CFrame.lookAt(charPos, v3(targetPos.X, charPos.Y, targetPos.Z)))
        wait()
        character:SetPrimaryPartCFrame(characterCf)
    end
end

-- // y axis 
loadstring(game:HttpGet("https://raw.githubusercontent.com/ozlbible/ozl/main/SilentAimAdvancements"))()

-- // auto mute boom box 

if Gult.Options.MuteBoomBox then
    for _, v in pairs(game:GetService("Workspace"):GetDescendants()) do
        if v:IsA("Sound") and not (v.Name == "ShootSound" or v.Name == "NoAmmo") then
            v.Volume = 0
        end
    end
end

-- // Auto low GFX

if Gult.Options.AutoLowGfx then
    for _, v in pairs(game:GetService("Workspace"):GetDescendants()) do
        if v:IsA("BasePart") and not v.Parent:FindFirstChild("Humanoid") then
            v.Material = Enum.Material.SmoothPlastic
            if v:IsA("Texture") then
                v:Destroy()
            end
        end
    end
end

-- // remove seats

if Gult.Options.RemoveSeats then
    for _, v in pairs(game:GetService("Workspace"):GetDescendants()) do
        if v:IsA("Seat") then
            v:Destroy()
        end
    end
end
end

-- // Texture \\ -- 

if getgenv().Gult.Texture.Enabled then
for _, v in pairs(game:GetService("Workspace"):GetDescendants()) do
    if v:IsA("BasePart") and not v.Parent:FindFirstChild("Humanoid") then
        v.Material = getgenv().Gult.Texture.Material
        v.Color = getgenv().Gult.Texture.Color
        if v:IsA("Texture") then
            v:Destroy()
        end
    end
end
end
end
