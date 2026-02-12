local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()
local Window = OrionLib:MakeWindow({Name = "เองคับ Hub | Auto Farm", HidePremium = false, SaveConfig = true, ConfigFolder = "EngKubConfig"})

-- ตัวแปรสำหรับเปิด/ปิดระบบ
_G.AutoFarm = false
_G.DistanceFarm = false

-- ฟังก์ชันสำหรับบินไปหามอนสเตอร์ (Tween)
function ToTarget(TargetLocation)
    local Character = game.Players.LocalPlayer.Character
    local Distance = (TargetLocation.Position - Character.HumanoidRootPart.Position).Magnitude
    local TweenService = game:GetService("TweenService")
    local Info = TweenInfo.new(Distance / 50, Enum.EasingStyle.Linear) -- ความเร็ว 50 (ปรับได้)
    local Tween = TweenService:Create(Character.HumanoidRootPart, Info, {CFrame = TargetLocation})
    Tween:Play()
end

-- สร้างเมนู
local Tab = Window:MakeTab({
	Name = "Auto Farm",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

-- ปุ่มเปิด/ปิด Auto Farm
Tab:AddToggle({
	Name = "Auto Farm (รับเควส + ตีมอน)",
	Default = false,
	Callback = function(Value)
		_G.AutoFarm = Value
        while _G.AutoFarm do
            task.wait(0.1)
            -- ตรงนี้เองคับต้องใส่ชื่อ NPC และชื่อมอนสเตอร์ของเกมนั้นๆ
            -- 1. รับเควส (ตัวอย่าง)
            -- game:GetService("ReplicatedStorage").Events.Quest:FireServer("MonsterName")
            
            -- 2. วาร์ปไปหามอนสเตอร์และตี
            -- ToTarget(game.Workspace.Monsters["MonsterName"].HumanoidRootPart.CFrame)
        end
	end    
})

-- ปุ่มตีระยะไกล
Tab:AddToggle({
	Name = "Auto Attack (ตีไกลอัตโนมัติ)",
	Default = false,
	Callback = function(Value)
		_G.DistanceFarm = Value
        while _G.DistanceFarm do
            task.wait(0.1)
            -- ใส่คำสั่งเรียกใช้สกิลหรือการคลิกโจมตีตรงนี้
            -- game:GetService("VirtualUser"):CaptureController()
            -- game:GetService("VirtualUser"):Button1Down(Vector2.new(0,0))
        end
	end    
})

OrionLib:Init()
