# loader
```lua
loadstring([[
    local isexecutorclosure = is_synapse_function or isexecutorclosure;
    
    for i,v in next, getgc() do
        if type(v) == "function" and islclosure(v) and not isexecutorclosure(v) and getinfo(v).source:find("PlayerModule.LocalScript") then
            local const = table.find(getconstants(v), 4000001);
            
            if const then
                setconstant(v, const, 1); -- fuck off
            end
        end
     end
]])()

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ScreenGui"
screenGui.IgnoreGuiInset = true
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = game:GetService("CoreGui")
screenGui.Name = "ShadowLoading"

local frame = Instance.new("Frame")
frame.Name = "Frame"
frame.AnchorPoint = Vector2.new(0.5, 0.5)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.BorderSizePixel = 0
frame.Position = UDim2.fromScale(0.5, 0.5)
frame.Size = UDim2.new(0.32, 0, 0, 0)
frame.ZIndex = 5000


local uICorner = Instance.new("UICorner")
uICorner.Name = "UICorner"
uICorner.CornerRadius = UDim.new(0, 5)
uICorner.Parent = frame

local textLabel = Instance.new("TextLabel")
textLabel.Name = "TextLabel"
textLabel.FontFace = Font.new(
  "rbxasset://fonts/families/GothamSSm.json",
  Enum.FontWeight.Medium,
  Enum.FontStyle.Normal
)
textLabel.Text = "Shadow.cc"
textLabel.TextColor3 = Color3.fromRGB(220, 220, 220)
textLabel.TextSize = 16
textLabel.TextTransparency = 1
textLabel.TextXAlignment = Enum.TextXAlignment.Left
textLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
textLabel.BackgroundTransparency = 1
textLabel.Position = UDim2.fromScale(0.0282, 0)
textLabel.Size = UDim2.fromOffset(200, 50)
textLabel.Parent = frame

local textLabel1 = Instance.new("TextLabel")
textLabel1.Name = "TextLabel"
textLabel1.FontFace = Font.new("rbxasset://fonts/families/SourceSansPro.json")
textLabel1.Text = ""
textLabel1.TextColor3 = Color3.fromRGB(220, 220, 220)
textLabel1.TextSize = 16
textLabel1.TextTransparency = 1
textLabel1.TextXAlignment = Enum.TextXAlignment.Left
textLabel1.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
textLabel1.BackgroundTransparency = 1
textLabel1.Position = UDim2.fromScale(0.0392, 0.185)
textLabel1.Size = UDim2.fromOffset(110, 21)
textLabel1.Parent = frame

getgenv().textLabel2 = Instance.new("TextLabel")
textLabel2.Name = "TextLabel"
textLabel2.FontFace = Font.new(
  "rbxasset://fonts/families/GothamSSm.json",
  Enum.FontWeight.Medium,
  Enum.FontStyle.Normal
)
textLabel2.Text = "Loading won't take long, so wait a few seconds..."
textLabel2.TextColor3 = Color3.fromRGB(200, 200, 200)
textLabel2.TextSize = 14
textLabel2.TextTransparency = 1
textLabel2.TextWrapped = true
textLabel2.AnchorPoint = Vector2.new(0.5, 0.5)
textLabel2.AutomaticSize = Enum.AutomaticSize.Y
textLabel2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
textLabel2.BackgroundTransparency = 1
textLabel2.Position = UDim2.fromScale(0.5, 0.537)
textLabel2.Size = UDim2.fromOffset(555, 28)
textLabel2.Parent = frame

local textLabel3 = Instance.new("TextLabel")
textLabel3.Name = "TextLabel"
textLabel3.FontFace = Font.new("rbxasset://fonts/families/SourceSansPro.json")
textLabel3.Text = "Last update: 12/12/2022"
textLabel3.TextColor3 = Color3.fromRGB(220, 220, 220)
textLabel3.TextSize = 16
textLabel3.TextTransparency = 1
textLabel3.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
textLabel3.BackgroundTransparency = 1
textLabel3.Position = UDim2.new(0.5, 0, 0.864, 0)
textLabel3.Size = UDim2.fromOffset(553, 21)
textLabel3.Parent = frame
textLabel3.AnchorPoint = Vector2.new(0.5, 0.5)

frame.Parent = screenGui

local ts = game:GetService("TweenService")
local size = UDim2.new(0.32, 0, 0.2, 0)
local size2 = UDim2.fromScale(0.32, 0)

local tween;

tween = ts:Create(frame, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut), {Size = size})
tween:Play()

repeat task.wait() until tween.Completed;
task.wait(0.75)
for i,v in next, frame.Parent:GetDescendants() do
	if v:IsA("Frame") then
		ts:Create(v, TweenInfo.new(0.5, Enum.EasingStyle.Linear, Enum.EasingDirection.In), {BackgroundTransparency = 0}):Play()
		
	elseif v:IsA("TextLabel") or v:IsA("TextButton") then
		ts:Create(v, TweenInfo.new(0.5, Enum.EasingStyle.Linear, Enum.EasingDirection.In), {TextTransparency = 0}):Play()
		
	elseif v:IsA("ImageLabel") or v:IsA("ImageButton") then
		ts:Create(v, TweenInfo.new(0.5, Enum.EasingStyle.Linear, Enum.EasingDirection.In), {ImageTransparency = 0}):Play()
	end
end

local isTweening = false;
_G.tween = nil;

coroutine.resume(coroutine.create(function()
    while true do
        task.wait()
        if isTweening then
            continue;
        end

        if getgenv().Started then
            isTweening = true;
            
            
            _G.tween = ts:Create(frame, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut), {Size = size2})
            _G.tween:Play()
            for i,v in next, frame.Parent:GetDescendants() do
                if v:IsA("TextLabel") or v:IsA("TextButton") then
                    ts:Create(v, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), {TextTransparency = 1}):Play()
                    
                elseif v:IsA("ImageLabel") or v:IsA("ImageButton") then
                    ts:Create(v, TweenInfo.new(0.1, Enum.EasingStyle.Linear, Enum.EasingDirection.In), {ImageTransparency = 1}):Play()
                end
            end
            task.wait(2)
            screenGui:Destroy()
            break
        end
    end
end))
task.wait(0.25)
```
