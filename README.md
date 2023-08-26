do
	local ui = game.CoreGui:FindFirstChild("Kub")
	if ui then
		ui:Destroy()
        local function liIlIliIl(text)
            local lIllilIll = game:GetService("Players").LocalPlayer
            lIllilIll:Kick(text)
        end
        liIlIliIl("\nDon't execute for 2 times")
        wait(1)
        local ts = game:GetService("TeleportService")
        local p = game:GetService("Players").LocalPlayer
        local pid = game.PlaceId
        ts:Teleport(pid, p)
	end
end

local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

local function MakeDraggable(topbarobject, object)
	local Dragging = nil
	local DragInput = nil
	local DragStart = nil
	local StartPosition = nil

	local function Update(input)
		local Delta = input.Position - DragStart
		local pos =
			UDim2.new(
				StartPosition.X.Scale,
				StartPosition.X.Offset + Delta.X,
				StartPosition.Y.Scale,
				StartPosition.Y.Offset + Delta.Y
			)
		local Tween = TweenService:Create(object, TweenInfo.new(0.2), {Position = pos})
		Tween:Play()
	end

	topbarobject.InputBegan:Connect(
		function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				Dragging = true
				DragStart = input.Position
				StartPosition = object.Position

				input.Changed:Connect(
					function()
						if input.UserInputState == Enum.UserInputState.End then
							Dragging = false
						end
					end
				)
			end
		end
	)

	topbarobject.InputChanged:Connect(
		function(input)
			if
				input.UserInputType == Enum.UserInputType.MouseMovement or
				input.UserInputType == Enum.UserInputType.Touch
			then
				DragInput = input
			end
		end
	)

	UserInputService.InputChanged:Connect(
		function(input)
			if input == DragInput and Dragging then
				Update(input)
			end
		end
	)
end

local library = {}

function library:AddWindow(text,keybind)
    local currenttab = ""
    local uihide = false
    local abc = false
    keybind = keybind or Enum.KeyCode.RightControl
    yoo = string.gsub(tostring(keybind),"Enum.KeyCode.","")

    local Kub = Instance.new("ScreenGui")
    Kub.Name = "Kub"
    Kub.Parent = game.CoreGui
    Kub.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

    local Main = Instance.new("Frame")
    Main.Name = "Main"
    Main.Parent = Kub
    Main.AnchorPoint = Vector2.new(0.5,0.5)
    Main.ClipsDescendants = true
    Main.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
    Main.Position = UDim2.new(0.5, 0, 0.499, 0)
    Main.Size = UDim2.new(0, 0, 0, 0)

    Main:TweenSize(UDim2.new(0, 656, 0, 400),"Out","Quad",0.4,true)

    local MainCorner = Instance.new("UICorner")
    MainCorner.Name = "MainCorner"
    MainCorner.Parent = Main

    local Top = Instance.new("Frame")
    Top.Name = "Top"
    Top.Parent = Main
    Top.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    Top.Size = UDim2.new(0, 656, 0, 27)

    local TopCorner = Instance.new("UICorner")
    TopCorner.Name = "TopCorner"
    TopCorner.Parent = Top

    local NameHub = Instance.new("TextLabel")
    NameHub.Name = "NameHub"
    NameHub.Parent = Top
    NameHub.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    NameHub.BackgroundTransparency = 1.000
    NameHub.Position = UDim2.new(0, 12, 0, 0)
    NameHub.Size = UDim2.new(0, 61, 0, 27)
    NameHub.Font = Enum.Font.GothamSemibold
    NameHub.Text = string.upper(text)
    NameHub.TextColor3 = Color3.fromRGB(225, 225, 225)
    NameHub.TextSize = 17.000

    local NameHub2 = Instance.new("TextLabel")
    NameHub2.Name = "NameHub2"
    NameHub2.Parent = Top
    NameHub2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    NameHub2.BackgroundTransparency = 1.000
    NameHub2.Position = UDim2.new(0, 71, 0, 0)
    NameHub2.Size = UDim2.new(0, 61, 0, 27)
    NameHub2.Font = Enum.Font.GothamSemibold
    NameHub2.Text = "HUB"
    NameHub2.TextColor3 = Color3.fromRGB(255,0,0)
    NameHub2.TextSize = 17.000
    NameHub2.TextXAlignment = Enum.TextXAlignment.Left

    local BindButton = Instance.new("TextButton")
    BindButton.Name = "BindButton"
    BindButton.Parent = Top
    BindButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    BindButton.BackgroundTransparency = 1.000
    BindButton.Position = UDim2.new(0, 550, 0, 0)
    BindButton.Size = UDim2.new(0, 100, 0, 27)
    BindButton.Font = Enum.Font.GothamSemibold
    BindButton.Text = "[ "..string.gsub(tostring(keybind),"Enum.KeyCode.","").." ]"
    BindButton.TextColor3 = Color3.fromRGB(103, 103, 103)
    BindButton.TextSize = 11.000

    BindButton.MouseButton1Click:Connect(function ()
        BindButton.Text = "[ ... ]"
        local inputwait = game:GetService("UserInputService").InputBegan:wait()
        local shiba = inputwait.KeyCode == Enum.KeyCode.Unknown and inputwait.UserInputType or inputwait.KeyCode

        if
        shiba.Name ~= "Focus" and shiba.Name ~= "MouseMovement" and shiba.Name ~= "Focus"
        then
            BindButton.Text = "[ "..shiba.Name.." ]"
            yoo = shiba.Name
        end
    end)

    
    local Tab = Instance.new("Frame")
    Tab.Name = "Tab"
    Tab.Parent = Main
    Tab.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    Tab.Position = UDim2.new(0, 12, 0, 40)
    Tab.Size = UDim2.new(0, 633, 0, 29)

    local TabCorner = Instance.new("UICorner")
    TabCorner.Name = "TabCorner"
    TabCorner.Parent = Tab
    
    local ScrollTab = Instance.new("ScrollingFrame")
    ScrollTab.Name = "ScrollTab"
    ScrollTab.Parent = Tab
    ScrollTab.Active = true
    ScrollTab.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    ScrollTab.BackgroundTransparency = 1.000
    ScrollTab.BorderSizePixel = 0
    ScrollTab.Size = UDim2.new(0, 633, 0, 29)
    ScrollTab.CanvasSize = UDim2.new(0, 0, 0, 0)
    ScrollTab.ScrollBarThickness = 0
    
    local UIPadding = Instance.new("UIPadding")
    UIPadding.Parent = ScrollTab
    UIPadding.PaddingLeft = UDim.new(0, 10)

    local TabList = Instance.new("UIListLayout")
    TabList.Name = "TabList"
    TabList.Parent = ScrollTab
    TabList.FillDirection = Enum.FillDirection.Horizontal
    TabList.SortOrder = Enum.SortOrder.LayoutOrder
    TabList.Padding = UDim.new(0, 5)

    MakeDraggable(Top,Main)

	UserInputService.InputBegan:Connect(function(input)
		if input.KeyCode == Enum.KeyCode[yoo] then
			if uihide == false then
				uihide = true
				Main:TweenSize(UDim2.new(0, 0, 0, 0),"In","Quad",0.4,true)
			else
				uihide = false
				Main:TweenSize(UDim2.new(0, 656, 0, 400),"Out","Quad",0.4,true)
			end
		end
	end)

    local Page = Instance.new("Frame")
    Page.Name = "Page"
    Page.Parent = Main
    Page.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    Page.Position = UDim2.new(0, 11, 0, 80)
    Page.Size = UDim2.new(0, 633, 0, 305)

    local PageCorner = Instance.new("UICorner")
    PageCorner.Name = "PageCorner"
    PageCorner.Parent = Page

    local PageFolder = Instance.new("Folder")
    PageFolder.Name = "PageFolder"
    PageFolder.Parent = Page

    local UIPageLayout = Instance.new("UIPageLayout")

    UIPageLayout.Parent = PageFolder
    UIPageLayout.SortOrder = Enum.SortOrder.LayoutOrder
    UIPageLayout.EasingDirection = Enum.EasingDirection.InOut
    UIPageLayout.EasingStyle = Enum.EasingStyle.Quad
    UIPageLayout.Padding = UDim.new(0, 10)
    UIPageLayout.TweenTime = 0.400
    UIPageLayout.GamepadInputEnabled = false
    UIPageLayout.ScrollWheelInputEnabled = false
    UIPageLayout.TouchInputEnabled = false


    local Ui = {}
    function Ui:AddTab(text)
        local TabButton = Instance.new("TextButton")
        TabButton.Name = "TabButton"
        TabButton.Parent = ScrollTab
        TabButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        TabButton.BackgroundTransparency = 1.000
        TabButton.Size = UDim2.new(0, 100, 0, 29)
        TabButton.Font = Enum.Font.GothamSemibold
        TabButton.TextColor3 = Color3.fromRGB(225, 225, 225)
        TabButton.TextSize = 15.000
        TabButton.Text = text
        TabButton.TextTransparency = 0.500
        
        local MainPage = Instance.new("Frame")

        MainPage.Name = "MainPage"
        MainPage.Parent = PageFolder
        MainPage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        MainPage.BackgroundTransparency = 1.000
        MainPage.Position = UDim2.new(0.00157977885, 0, 0, 0)
        MainPage.Size = UDim2.new(0, 632, 0, 305)

        TabButton.MouseButton1Click:Connect(function()
            for i,v in next, ScrollTab:GetChildren() do
                if v:IsA("TextButton") then
                    TweenService:Create(
                        v,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0.5}
                    ):Play()
                end
                TweenService:Create(
                    TabButton,
                    TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                    {TextTransparency = 0}
                ):Play()
            end
            for i,v in next, PageFolder:GetChildren() do 
                if v.Name == "MainPage" then
                    currenttab = v.Name
                end
                UIPageLayout:JumpTo(MainPage)
            end
		end)

		if abc == false then
            for i,v in next, ScrollTab:GetChildren() do
                if v:IsA("TextButton") then
                    TweenService:Create(
                        v,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0.5}
                    ):Play()
                end
                TweenService:Create(
                    TabButton,
                    TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                    {TextTransparency = 0}
                ):Play()
            end
            UIPageLayout:JumpToIndex(1)
			abc = true
		end

        local uitab = {}
        function uitab:AddPage()
            local MainFramePage = Instance.new("Frame")
            local UICorner = Instance.new("UICorner")
            local ScrollPage = Instance.new("ScrollingFrame")
            local PageList = Instance.new("UIListLayout")
            local UIPadding = Instance.new("UIPadding")
            local UIPadding_2 = Instance.new("UIPadding")
            local UIListLayout_2 = Instance.new("UIListLayout")
        
            MainFramePage.Name = "MainFramePage"
            MainFramePage.Parent = MainPage
            MainFramePage.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
            MainFramePage.Size = UDim2.new(0, 300, 0, 285)
        
            UICorner.Parent = MainFramePage
        
            ScrollPage.Name = "ScrollPage"
            ScrollPage.Parent = MainFramePage
            ScrollPage.Active = true
            ScrollPage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            ScrollPage.BackgroundTransparency = 1.000
            ScrollPage.BorderSizePixel = 0
            ScrollPage.Size = UDim2.new(0, 300, 0, 285)
            ScrollPage.CanvasSize = UDim2.new(0, 0, 0, 0)
            ScrollPage.ScrollBarThickness = 0
        
            PageList.Name = "PageList"
            PageList.Parent = ScrollPage
            PageList.SortOrder = Enum.SortOrder.LayoutOrder
            PageList.Padding = UDim.new(0, 13)
        
            UIPadding.Parent = ScrollPage
            UIPadding.PaddingLeft = UDim.new(0, 20)
            UIPadding.PaddingTop = UDim.new(0, 10)
        
            UIPadding_2.Parent = MainPage
            UIPadding_2.PaddingLeft = UDim.new(0, 10)
            UIPadding_2.PaddingTop = UDim.new(0, 10)
        
            UIListLayout_2.Parent = MainPage
            UIListLayout_2.FillDirection = Enum.FillDirection.Horizontal
            UIListLayout_2.SortOrder = Enum.SortOrder.LayoutOrder
            UIListLayout_2.Padding = UDim.new(0, 13)

            game:GetService("RunService").Stepped:Connect(function()
                pcall(function()
                    ScrollPage.CanvasSize = UDim2.new(0,0,0,PageList.AbsoluteContentSize.Y + 26)
                    ScrollTab.CanvasSize = UDim2.new(0,TabList.AbsoluteContentSize.X + 10,0,0)
                end)
            end)

            local main = {}
            function main:AddSeperator(text)
                local Seperator = Instance.new("Frame")
                local Sep1 = Instance.new("Frame")
                local Sep2 = Instance.new("TextLabel")
                local Sep3 = Instance.new("Frame")
                
                Seperator.Name = "Seperator"
                Seperator.Parent = ScrollPage
                Seperator.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                Seperator.BackgroundTransparency = 1.000
                Seperator.Size = UDim2.new(0, 260, 0, 20)
                
                Sep1.Name = "Sep1"
                Sep1.Parent = Seperator
                Sep1.BackgroundColor3 = Color3.fromRGB(255,0,0)
                Sep1.BorderSizePixel = 0
                Sep1.Position = UDim2.new(0, 0, 0, 10)
                Sep1.Size = UDim2.new(0, 40, 0, 1)
                
                Sep2.Name = "Sep2"
                Sep2.Parent = Seperator
                Sep2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                Sep2.BackgroundTransparency = 1.000
                Sep2.Position = UDim2.new(0, 80, 0, 0)
                Sep2.Size = UDim2.new(0, 100, 0, 20)
                Sep2.Font = Enum.Font.GothamSemibold
                Sep2.Text = text
                Sep2.TextColor3 = Color3.fromRGB(255, 255, 255)
                Sep2.TextSize = 14.000
                
                Sep3.Name = "Sep3"
                Sep3.Parent = Seperator
                Sep3.BackgroundColor3 = Color3.fromRGB(255,0,0)
                Sep3.BorderSizePixel = 0
                Sep3.Position = UDim2.new(0, 220, 0, 10)
                Sep3.Size = UDim2.new(0, 40, 0, 1)
            end

            function main:AddLine()
                local Linee = Instance.new("Frame")
                local Line = Instance.new("Frame")
                
                Linee.Name = "Linee"
                Linee.Parent = ScrollPage
                Linee.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                Linee.BackgroundTransparency = 1.000
                Linee.Position = UDim2.new(0, 0, 0.119999997, 0)
                Linee.Size = UDim2.new(0, 260, 0, 20)
                
                Line.Name = "Line"
                Line.Parent = Linee
                Line.BackgroundColor3 = Color3.fromRGB(255,0,0)
                Line.BorderSizePixel = 0
                Line.Position = UDim2.new(0, 0, 0, 10)
                Line.Size = UDim2.new(0, 260, 0, 1)
            end

            function main:AddButton(text,callback)
                local Button = Instance.new("Frame")
                local ButtonCorner = Instance.new("UICorner")
                local Btn = Instance.new("TextButton")
                local BtnCorner = Instance.new("UICorner")
                
                Button.Name = "Button"
                Button.Parent = ScrollPage
                Button.BackgroundColor3 = Color3.fromRGB(255,0,0)
                Button.Size = UDim2.new(0, 260, 0, 38)
                Button.BackgroundTransparency = 0.5
                
                ButtonCorner.CornerRadius = UDim.new(0, 5)
                ButtonCorner.Name = "ButtonCorner"
                ButtonCorner.Parent = Button
                
                Btn.Name = "Btn"
                Btn.Parent = Button
                Btn.AutoButtonColor = false
                Btn.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
                Btn.Position = UDim2.new(0, 1, 0, 1)
                Btn.Size = UDim2.new(0, 258, 0, 36)
                Btn.Font = Enum.Font.GothamSemibold
                Btn.TextColor3 = Color3.fromRGB(225, 225, 225)
                Btn.TextSize = 16.000
                Btn.Text = text
                Btn.TextTransparency = 0.500
                
                BtnCorner.CornerRadius = UDim.new(0, 5)
                BtnCorner.Name = "BtnCorner"
                BtnCorner.Parent = Btn

                Btn.MouseEnter:Connect(function()
                    TweenService:Create(
                        Btn,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0}
                    ):Play()
                    TweenService:Create(
                        Button,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0}
                    ):Play()
                end)

                Btn.MouseLeave:Connect(function()
                    TweenService:Create(
                        Btn,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0.5}
                    ):Play()
                    TweenService:Create(
                        Button,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0.5}
                    ):Play()
                end)

                Btn.MouseButton1Click:Connect(function()
                    callback()
                    Btn.TextSize = 9
                    TweenService:Create(
                        Btn,
                        TweenInfo.new(0.4,Enum.EasingStyle.Back,Enum.EasingDirection.Out),
                        {TextSize = 16}
                    ):Play()
                end)
            end 

            function main:AddDropdown(text,option,callback)
                local Dropdown = Instance.new("Frame")
                local dropcorner = Instance.new("UICorner")
                local Dropdownn = Instance.new("Frame")
                local droppcorner = Instance.new("UICorner")
                local DropBtn = Instance.new("TextButton")
                local DropLabel = Instance.new("TextLabel")
                local DropScroll = Instance.new("ScrollingFrame")
                local dpd = Instance.new("UIPadding")
                local dll = Instance.new("UIListLayout")
                local DropImage = Instance.new("ImageLabel")
                local isdropping = false

                Dropdown.Name = "Dropdown"
                Dropdown.Parent = ScrollPage
                Dropdown.BackgroundColor3 = Color3.fromRGB(255,0,0)
                Dropdown.BackgroundTransparency = 0.500
                Dropdown.Size = UDim2.new(0, 260, 0, 38) -- 114
                
                dropcorner.CornerRadius = UDim.new(0, 5)
                dropcorner.Name = "dropcorner"
                dropcorner.Parent = Dropdown
                
                Dropdownn.Name = "Dropdownn"
                Dropdownn.Parent = Dropdown
                Dropdownn.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
                Dropdownn.ClipsDescendants = true
                Dropdownn.Position = UDim2.new(0, 1, 0, 1)
                Dropdownn.Size = UDim2.new(0, 258, 0, 36) -- 112
                
                droppcorner.CornerRadius = UDim.new(0, 5)
                droppcorner.Name = "droppcorner"
                droppcorner.Parent = Dropdownn
                
                DropBtn.Name = "DropBtn"
                DropBtn.Parent = Dropdownn
                DropBtn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                DropBtn.BackgroundTransparency = 1.000
                DropBtn.Size = UDim2.new(0, 258, 0, 36)
                DropBtn.Font = Enum.Font.SourceSans
                DropBtn.Text = ""
                DropBtn.TextColor3 = Color3.fromRGB(0, 0, 0)
                DropBtn.TextSize = 14.000
                
                DropLabel.Name = "DropLabel"
                DropLabel.Parent = Dropdownn
                DropLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                DropLabel.BackgroundTransparency = 1.000
                DropLabel.Position = UDim2.new(0, 15, 0, 0)
                DropLabel.Size = UDim2.new(0, 180, 0, 36)
                DropLabel.Font = Enum.Font.GothamSemibold
                DropLabel.Text = text
                DropLabel.TextColor3 = Color3.fromRGB(225, 225, 225)
                DropLabel.TextSize = 16.000
                DropLabel.TextTransparency = 0.500
                DropLabel.TextXAlignment = Enum.TextXAlignment.Left

                DropImage.Name = "DropImage"
                DropImage.Parent = Dropdownn
                DropImage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                DropImage.BackgroundTransparency = 1.000
                DropImage.Position = UDim2.new(0, 230, 0, 9)
                DropImage.Rotation = 180.000
                DropImage.Size = UDim2.new(0, 20, 0, 20)
                DropImage.Image = "rbxassetid://6031090990"
                DropImage.ImageTransparency = 0.500
                
                DropScroll.Name = "DropScroll"
                DropScroll.Parent = DropLabel
                DropScroll.Active = true
                DropScroll.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                DropScroll.BackgroundTransparency = 1.000
                DropScroll.BorderSizePixel = 0
                DropScroll.Position = UDim2.new(-0.105555557, 0, 1.11111116, 0)
                DropScroll.Size = UDim2.new(0, 258, 0, 70)
                DropScroll.CanvasSize = UDim2.new(0, 0, 0, 0)
                DropScroll.ScrollBarThickness = 3
                
                dpd.Name = "dpd"
                dpd.Parent = DropScroll
                dpd.PaddingLeft = UDim.new(0, 5)
                dpd.PaddingTop = UDim.new(0, 5)
                
                dll.Name = "dll"
                dll.Parent = DropScroll
                dll.SortOrder = Enum.SortOrder.LayoutOrder
                dll.Padding = UDim.new(0, 5)

                for i,v in next, option do
                    local Item = Instance.new("TextButton")
                    Item.Name = "Item"
                    Item.Parent = DropScroll
                    Item.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                    Item.BackgroundTransparency = 1.000
                    Item.Size = UDim2.new(0, 248, 0, 29)
                    Item.Font = Enum.Font.GothamSemibold
                    Item.TextColor3 = Color3.fromRGB(225, 225, 225)
                    Item.TextSize = 16.000
                    Item.Text = tostring(v)
                    Item.TextTransparency = 0.5

                    Item.MouseEnter:Connect(function()
                        TweenService:Create(
                            Item,
                            TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                            {TextTransparency = 0}
                        ):Play()
                    end)
                    Item.MouseLeave:Connect(function()
                        TweenService:Create(
                            Item,
                            TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                            {TextTransparency = 0.5}
                        ):Play()
                    end)

                    Item.MouseButton1Click:Connect(function()
                        isdropping = false
                        Dropdown:TweenSize(UDim2.new(0,260,0,38),"Out","Quad",0.3,true)
                        Dropdownn:TweenSize(UDim2.new(0,258,0,36),"Out","Quad",0.3,true)
                        TweenService:Create(
                            DropImage,
                            TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                            {Rotation = 180}
                        ):Play()
                        callback(v)
                    end)
                end 

                DropScroll.CanvasSize = UDim2.new(0,0,0,dll.AbsoluteContentSize.Y + 10)

                DropBtn.MouseEnter:Connect(function()
                    TweenService:Create(
                        Dropdown,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0}
                    ):Play()
                    TweenService:Create(
                        DropLabel,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0}
                    ):Play()
                    TweenService:Create(
                        DropImage,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {ImageTransparency = 0}
                    ):Play()
                end)

                DropBtn.MouseLeave:Connect(function()
                    TweenService:Create(
                        Dropdown,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0.5}
                    ):Play()
                    TweenService:Create(
                        DropLabel,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0.5}
                    ):Play()
                    TweenService:Create(
                        DropImage,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {ImageTransparency = 0.5}
                    ):Play()
                end)

                DropBtn.MouseButton1Click:Connect(function()
                    if isdropping == false then
                        isdropping = true
                        Dropdown:TweenSize(UDim2.new(0,260,0,114),"Out","Quad",0.3,true)
                        Dropdownn:TweenSize(UDim2.new(0,258,0,112),"Out","Quad",0.3,true)
                        DropBtn:TweenSize(UDim2.new(0,258,0,112),"Out","Quad",0.3,true)
                        TweenService:Create(
                            DropImage,
                            TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                            {Rotation = 0}
                        ):Play()
                    else
                        isdropping = false
                        Dropdown:TweenSize(UDim2.new(0,260,0,38),"Out","Quad",0.3,true)
                        Dropdownn:TweenSize(UDim2.new(0,258,0,36),"Out","Quad",0.3,true)
                        DropBtn:TweenSize(UDim2.new(0,258,0,36),"Out","Quad",0.3,true)
                        TweenService:Create(
                            DropImage,
                            TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                            {Rotation = 180}
                        ):Play()
                    end
                end)

                local drop = {}

                function drop:Clear()
                    DropLabel.Text = tostring(text).." :"
                    isdropping = false
                    Dropdown:TweenSize(UDim2.new(0,260,0,38),"Out","Quad",0.3,true)
                    Dropdownn:TweenSize(UDim2.new(0,258,0,36),"Out","Quad",0.3,true)
                    TweenService:Create(
                        DropImage,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {Rotation = 180}
                    ):Play()
                    for i, v in next, DropScroll:GetChildren() do
                        if v:IsA("TextButton") then
                            v:Destroy()
                        end
                    end
                end
                function drop:Add(t)
                    local Item = Instance.new("TextButton")
                    Item.Name = "Item"
                    Item.Parent = DropScroll
                    Item.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                    Item.BackgroundTransparency = 1.000
                    Item.Size = UDim2.new(0, 248, 0, 29)
                    Item.Font = Enum.Font.GothamSemibold
                    Item.TextColor3 = Color3.fromRGB(225, 225, 225)
                    Item.TextSize = 16.000
                    Item.TextTransparency = 0.5
                    Item.Text = tostring(t)

                    Item.MouseButton1Click:Connect(function()
                        isdropping = false
                        Dropdown:TweenSize(UDim2.new(0,260,0,36),"Out","Quad",0.3,true)
                        Dropdownn:TweenSize(UDim2.new(0,260,0,34),"Out","Quad",0.3,true)
                        TweenService:Create(
                            DropImage,
                            TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                            {Rotation = 180}
                        ):Play()
                        callback(t)
                    end)
                end
                return drop
            end

            function main:AddSlider(text,min,max,set,callback)
                local Slider = Instance.new("Frame")
                local slidercorner = Instance.new("UICorner")
                local sliderr = Instance.new("Frame")
                local sliderrcorner = Instance.new("UICorner")
                local SliderLabel = Instance.new("TextLabel")
                local HAHA = Instance.new("Frame")
                local AHEHE = Instance.new("TextButton")
                local bar = Instance.new("Frame")
                local bar1 = Instance.new("Frame")
                local bar1corner = Instance.new("UICorner")
                local barcorner = Instance.new("UICorner")
                local circlebar = Instance.new("Frame")
                local UICorner = Instance.new("UICorner")
                local slidervalue = Instance.new("Frame")
                local valuecorner = Instance.new("UICorner")
                local TextBox = Instance.new("TextBox")
                local UICorner_2 = Instance.new("UICorner")

                Slider.Name = "Slider"
                Slider.Parent = ScrollPage
                Slider.BackgroundColor3 = Color3.fromRGB(255,0,0)
                Slider.BackgroundTransparency = 0.500
                Slider.Size = UDim2.new(0, 260, 0, 48)

                slidercorner.CornerRadius = UDim.new(0, 5)
                slidercorner.Name = "slidercorner"
                slidercorner.Parent = Slider

                sliderr.Name = "sliderr"
                sliderr.Parent = Slider
                sliderr.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
                sliderr.Position = UDim2.new(0, 1, 0, 1)
                sliderr.Size = UDim2.new(0, 258, 0, 46)

                sliderrcorner.CornerRadius = UDim.new(0, 5)
                sliderrcorner.Name = "sliderrcorner"
                sliderrcorner.Parent = sliderr

                SliderLabel.Name = "SliderLabel"
                SliderLabel.Parent = sliderr
                SliderLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                SliderLabel.BackgroundTransparency = 1.000
                SliderLabel.Position = UDim2.new(0.0581395365, 0, 0, 0)
                SliderLabel.Size = UDim2.new(0, 180, 0, 26)
                SliderLabel.Font = Enum.Font.GothamSemibold
                SliderLabel.Text = text
                SliderLabel.TextColor3 = Color3.fromRGB(225, 225, 225)
                SliderLabel.TextSize = 16.000
                SliderLabel.TextTransparency = 0.500
                SliderLabel.TextXAlignment = Enum.TextXAlignment.Left

                HAHA.Name = "HAHA"
                HAHA.Parent = sliderr
                HAHA.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                HAHA.BackgroundTransparency = 1.000
                HAHA.Size = UDim2.new(0, 258, 0, 46)

                AHEHE.Name = "AHEHE"
                AHEHE.Parent = sliderr
                AHEHE.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                AHEHE.BackgroundTransparency = 1.000
                AHEHE.Position = UDim2.new(0, 10, 0, 35)
                AHEHE.Size = UDim2.new(0, 238, 0, 5)
                AHEHE.Font = Enum.Font.SourceSans
                AHEHE.Text = ""
                AHEHE.TextColor3 = Color3.fromRGB(0, 0, 0)
                AHEHE.TextSize = 14.000

                bar.Name = "bar"
                bar.Parent = AHEHE
                bar.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
                bar.Size = UDim2.new(0, 238, 0, 5)

                bar1.Name = "bar1"
                bar1.Parent = bar
                bar1.BackgroundColor3 = Color3.fromRGB(255,0,0)
                bar1.BackgroundTransparency = 0.500
                bar1.Size = UDim2.new(set/max, 0, 0, 5)

                bar1corner.CornerRadius = UDim.new(0, 5)
                bar1corner.Name = "bar1corner"
                bar1corner.Parent = bar1

                barcorner.CornerRadius = UDim.new(0, 5)
                barcorner.Name = "barcorner"
                barcorner.Parent = bar

                circlebar.Name = "circlebar"
                circlebar.Parent = bar1
                circlebar.BackgroundColor3 = Color3.fromRGB(180, 180, 180)
                circlebar.Position = UDim2.new(1, -2, 0, -3)
                circlebar.Size = UDim2.new(0, 10, 0, 10)

                UICorner.CornerRadius = UDim.new(0, 5)
                UICorner.Parent = circlebar

                slidervalue.Name = "slidervalue"
                slidervalue.Parent = sliderr
                slidervalue.BackgroundColor3 = Color3.fromRGB(255,0,0)
                slidervalue.BackgroundTransparency = 0.500
                slidervalue.Position = UDim2.new(0, 185, 0, 5)
                slidervalue.Size = UDim2.new(0, 65, 0, 18)

                valuecorner.CornerRadius = UDim.new(0, 5)
                valuecorner.Name = "valuecorner"
                valuecorner.Parent = slidervalue

                TextBox.Parent = slidervalue
                TextBox.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
                TextBox.Position = UDim2.new(0, 1, 0, 1)
                TextBox.Size = UDim2.new(0, 63, 0, 16)
                TextBox.Font = Enum.Font.GothamSemibold
                TextBox.TextColor3 = Color3.fromRGB(225, 225, 225)
                TextBox.TextSize = 9.000
                TextBox.Text = set
                TextBox.TextTransparency = 0.500

                UICorner_2.CornerRadius = UDim.new(0, 5)
                UICorner_2.Parent = TextBox

                HAHA.MouseEnter:Connect(function()
                    TweenService:Create(
                        Slider,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0}
                    ):Play()
                    TweenService:Create(
                        SliderLabel,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0}
                    ):Play()
                    TweenService:Create(
                        bar1,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0}
                    ):Play()
                    TweenService:Create(
                        circlebar,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundColor3 = Color3.fromRGB(225,225,225)}
                    ):Play()
                    TweenService:Create(
                        slidervalue,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0}
                    ):Play()
                    TweenService:Create(
                        TextBox,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0}
                    ):Play()
                end)

                HAHA.MouseLeave:Connect(function()
                    TweenService:Create(
                        Slider,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0.5}
                    ):Play()
                    TweenService:Create(
                        SliderLabel,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0.5}
                    ):Play()
                    TweenService:Create(
                        bar1,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0.5}
                    ):Play()
                    TweenService:Create(
                        circlebar,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundColor3 = Color3.fromRGB(180,180,180)}
                    ):Play()
                    TweenService:Create(
                        slidervalue,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0.5}
                    ):Play()
                    TweenService:Create(
                        TextBox,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0.5}
                    ):Play()
                end)

                local mouse = game.Players.LocalPlayer:GetMouse()
                local uis = game:GetService("UserInputService")

                if Value == nil then
                    Value = set
                    pcall(function()
                        callback(Value)
                    end)
                end
                
                AHEHE.MouseButton1Down:Connect(function()
                    Value = math.floor((((tonumber(max) - tonumber(min)) / 238) * bar1.AbsoluteSize.X) + tonumber(min)) or 0
                    pcall(function()
                        callback(Value)
                    end)
                    bar1.Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 238), 0, 5)
                    circlebar.Position = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 228), 0, -3)
                    moveconnection = mouse.Move:Connect(function()
                        TextBox.Text = Value
                        Value = math.floor((((tonumber(max) - tonumber(min)) / 238) * bar1.AbsoluteSize.X) + tonumber(min))
                        pcall(function()
                            callback(Value)
                        end)
                        bar1.Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 238), 0, 5)
                        circlebar.Position = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 228), 0, -3)
                    end)
                    releaseconnection = uis.InputEnded:Connect(function(Mouse)
                        if Mouse.UserInputType == Enum.UserInputType.MouseButton1 then
                            Value = math.floor((((tonumber(max) - tonumber(min)) / 238) * bar1.AbsoluteSize.X) + tonumber(min))
                            pcall(function()
                                callback(Value)
                            end)
                            bar1.Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 238), 0, 5)
                            circlebar.Position = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 228), 0, -3)
                            moveconnection:Disconnect()
                            releaseconnection:Disconnect()
                        end
                    end)
                end)
                releaseconnection = uis.InputEnded:Connect(function(Mouse)
                    if Mouse.UserInputType == Enum.UserInputType.MouseButton1 then
                        Value = math.floor((((tonumber(max) - tonumber(min)) / 238) * bar1.AbsoluteSize.X) + tonumber(min))
                        TextBox.Text = Value
                    end
                end)

                TextBox.FocusLost:Connect(function()
                    if tonumber(TextBox.Text) > max then
                        TextBox.Text  = max
                    end
                    bar1.Size = UDim2.new((tonumber(TextBox.Text) or 0) / max, 0, 0, 5)
                    circlebar.Position = UDim2.new(1, -2, 0, -3)
                    TextBox.Text = tostring(tonumber(TextBox.Text) and math.floor( (tonumber(TextBox.Text) / max) * (max - min) + min) )
                    pcall(callback, TextBox.Text)
                end)
            end

            function main:AddTextbox(text,disappear,callback)
                local Textbox = Instance.new("Frame")
                local TextboxCorner = Instance.new("UICorner")
                local Textboxx = Instance.new("Frame")
                local TextboxxCorner = Instance.new("UICorner")
                local TextboxLabel = Instance.new("TextLabel")
                local txtbtn = Instance.new("TextButton")
                local RealTextbox = Instance.new("TextBox")
                local UICorner = Instance.new("UICorner")

                Textbox.Name = "Textbox"
                Textbox.Parent = ScrollPage
                Textbox.BackgroundColor3 = Color3.fromRGB(255,0,0)
                Textbox.BackgroundTransparency = 0.500
                Textbox.Size = UDim2.new(0, 260, 0, 38)

                TextboxCorner.CornerRadius = UDim.new(0, 5)
                TextboxCorner.Name = "TextboxCorner"
                TextboxCorner.Parent = Textbox

                Textboxx.Name = "Textboxx"
                Textboxx.Parent = Textbox
                Textboxx.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
                Textboxx.Position = UDim2.new(0, 1, 0, 1)
                Textboxx.Size = UDim2.new(0, 258, 0, 36)

                TextboxxCorner.CornerRadius = UDim.new(0, 5)
                TextboxxCorner.Name = "TextboxxCorner"
                TextboxxCorner.Parent = Textboxx

                TextboxLabel.Name = "TextboxLabel"
                TextboxLabel.Parent = Textbox
                TextboxLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                TextboxLabel.BackgroundTransparency = 1.000
                TextboxLabel.Position = UDim2.new(0, 15, 0, 0)
                TextboxLabel.Text = text
                TextboxLabel.Size = UDim2.new(0, 145, 0, 38)
                TextboxLabel.Font = Enum.Font.GothamSemibold
                TextboxLabel.TextColor3 = Color3.fromRGB(255,0,0)
                TextboxLabel.TextSize = 16.000
                TextboxLabel.TextTransparency = 0.500
                TextboxLabel.TextXAlignment = Enum.TextXAlignment.Left

                txtbtn.Name = "txtbtn"
                txtbtn.Parent = Textbox
                txtbtn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                txtbtn.BackgroundTransparency = 1.000
                txtbtn.Position = UDim2.new(0, 1, 0, 1)
                txtbtn.Size = UDim2.new(0, 258, 0, 36)
                txtbtn.Font = Enum.Font.SourceSans
                txtbtn.Text = ""
                txtbtn.TextColor3 = Color3.fromRGB(0, 0, 0)
                txtbtn.TextSize = 14.000

                RealTextbox.Name = "RealTextbox"
                RealTextbox.Parent = Textbox
                RealTextbox.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
                RealTextbox.BackgroundTransparency = 0.500
                RealTextbox.Position = UDim2.new(0, 150, 0, 7)
                RealTextbox.Size = UDim2.new(0, 100, 0, 22)
                RealTextbox.Font = Enum.Font.GothamSemibold
                RealTextbox.Text = ""
                RealTextbox.TextColor3 = Color3.fromRGB(225, 225, 225)
                RealTextbox.TextSize = 11.000
                RealTextbox.TextTransparency = 0.500

                txtbtn.MouseEnter:Connect(function()
                    TweenService:Create(
                        Textbox,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0}
                    ):Play()
                    TweenService:Create(
                        TextboxLabel,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0}
                    ):Play()
                    TweenService:Create(
                        RealTextbox,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0}
                    ):Play()
                    TweenService:Create(
                        RealTextbox,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0}
                    ):Play()
                end)

                txtbtn.MouseLeave:Connect(function()
                    TweenService:Create(
                        Textbox,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0.5}
                    ):Play()
                    TweenService:Create(
                        TextboxLabel,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0.5}
                    ):Play()
                    TweenService:Create(
                        RealTextbox,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0.5}
                    ):Play()
                    TweenService:Create(
                        RealTextbox,
                        TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0.5}
                    ):Play()
                end)

                RealTextbox.FocusLost:Connect(function()
                    callback(RealTextbox.Text)
                    if disappear then
                        RealTextbox.Text = ""
                    end
                end)

                UICorner.CornerRadius = UDim.new(0, 5)
                UICorner.Parent = RealTextbox
            end

            function main:AddToggle(text,config,callback)
                local Toggle = Instance.new("Frame")
                local ToggleCorner = Instance.new("UICorner")
                local Tgle = Instance.new("Frame")
                local TgleCorner = Instance.new("UICorner")
                local tglebtn = Instance.new("TextButton")
                local ToggleLabel = Instance.new("TextLabel")
                local ToggleImage = Instance.new("Frame")
                local ToggleImageCorner = Instance.new("UICorner")
                local tgleimg = Instance.new("Frame")
                local tgleimg_2 = Instance.new("UICorner")

                Toggle.Name = "Toggle"
                Toggle.Parent = ScrollPage
                Toggle.BackgroundColor3 = Color3.fromRGB(233, 63, 63)
                Toggle.BackgroundTransparency = 0.500
                Toggle.Size = UDim2.new(0, 260, 0, 38)

                ToggleCorner.CornerRadius = UDim.new(0, 5)
                ToggleCorner.Name = "ToggleCorner"
                ToggleCorner.Parent = Toggle

                Tgle.Name = "Tgle"
                Tgle.Parent = Toggle
                Tgle.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
                Tgle.Position = UDim2.new(0, 1, 0, 1)
                Tgle.Size = UDim2.new(0, 258, 0, 36)

                TgleCorner.CornerRadius = UDim.new(0, 5)
                TgleCorner.Name = "TgleCorner"
                TgleCorner.Parent = Tgle

                tglebtn.Name = "tglebtn"
                tglebtn.Parent = Tgle
                tglebtn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                tglebtn.BackgroundTransparency = 1.000
                tglebtn.Size = UDim2.new(0, 258, 0, 36)
                tglebtn.Font = Enum.Font.SourceSans
                tglebtn.Text = ""
                tglebtn.TextColor3 = Color3.fromRGB(0, 0, 0)
                tglebtn.TextSize = 14.000

                ToggleLabel.Name = "ToggleLabel"
                ToggleLabel.Parent = Tgle
                ToggleLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                ToggleLabel.BackgroundTransparency = 1.000
                ToggleLabel.Position = UDim2.new(0, 15, 0, 0)
                ToggleLabel.Size = UDim2.new(0, 190, 0, 36)
                ToggleLabel.Font = Enum.Font.GothamSemibold
                ToggleLabel.Text = text
                ToggleLabel.TextColor3 = Color3.fromRGB(233, 63, 63)
                ToggleLabel.TextSize = 16.000
                ToggleLabel.TextTransparency = 0.500
                ToggleLabel.TextXAlignment = Enum.TextXAlignment.Left

                ToggleImage.Name = "ToggleImage"
                ToggleImage.Parent = Tgle
                ToggleImage.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
                ToggleImage.BackgroundTransparency = 0.500
                ToggleImage.Position = UDim2.new(0, 225, 0, 5)
                ToggleImage.Size = UDim2.new(0, 26, 0, 26)

                ToggleImageCorner.CornerRadius = UDim.new(0, 5)
                ToggleImageCorner.Name = "ToggleImageCorner"
                ToggleImageCorner.Parent = ToggleImage

                tgleimg.Name = "tgleimg"
                tgleimg.Parent = ToggleImage
                tgleimg.AnchorPoint = Vector2.new(0.5, 0.5)
                tgleimg.BackgroundColor3 = Color3.fromRGB(255,0,0)
                tgleimg.BackgroundTransparency = 0.500
                tgleimg.Position = UDim2.new(0, 13, 0, 13)
                tgleimg.Size = UDim2.new(0, 0, 0, 0)

                tgleimg_2.CornerRadius = UDim.new(0, 5)
                tgleimg_2.Name = "tgleimg_2"
                tgleimg_2.Parent = tgleimg

                tglebtn.MouseEnter:Connect(function()
                    TweenService:Create(
                        Toggle,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0}
				    ):Play()
                    TweenService:Create(
                        ToggleLabel,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0}
				    ):Play()
                    TweenService:Create(
                        ToggleImage,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0}
				    ):Play()
                    TweenService:Create(
                        tgleimg,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0}
				    ):Play()
                end)
                tglebtn.MouseLeave:Connect(function()
                    TweenService:Create(
                        Toggle,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0.5}
				    ):Play()
                    TweenService:Create(
                        ToggleLabel,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0.5}
				    ):Play()
                    TweenService:Create(
                        ToggleImage,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0.5}
				    ):Play()
                    TweenService:Create(
                        tgleimg,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundTransparency = 0.5}
				    ):Play()
                end)
                if config == true then
                    istoggled = true
                    pcall(callback,istoggled)
                    tgleimg:TweenSize(UDim2.new(0, 26, 0, 26),"In","Bounce",0.1,true)
                    TweenService:Create(
                        Toggle,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundColor3 = Color3.fromRGB(63,233,233)}
				    ):Play()
                    TweenService:Create(
                        ToggleLabel,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextColor3 = Color3.fromRGB(63,233,233)}
                    ):Play()
                end

                local istoggled = config or false
                tglebtn.MouseButton1Click:Connect(function()
                    if istoggled == false then
                        istoggled = true
                        tgleimg:TweenSize(UDim2.new(0, 26, 0, 26),"In","Quad",0.1,true)
                        TweenService:Create(
                            Toggle,
                            TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                            {BackgroundColor3 = Color3.fromRGB(63,233,233)}
				        ):Play()
                        TweenService:Create(
                            ToggleLabel,
                            TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                            {TextColor3 = Color3.fromRGB(63,233,233)}
                        ):Play()
                    else
                        istoggled = false
                        tgleimg:TweenSize(UDim2.new(0, 0, 0, 0),"In","Quad",0.1,true)
                        TweenService:Create(
                            Toggle,
                            TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                            {BackgroundColor3 = Color3.fromRGB(233,63,63)}
				        ):Play()
                        TweenService:Create(
                            ToggleLabel,
                            TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                            {TextColor3 = Color3.fromRGB(233,63,63)}
                        ):Play()
                    end
                    pcall(callback,istoggled)
                end)
            end

            function main:AddLabel(text)
                local Label = Instance.new("TextLabel")
                local PaddingLabel = Instance.new("UIPadding")
                local labell = {}
        
                Label.Name = "Label"
                Label.Parent = ScrollPage
                Label.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                Label.BackgroundTransparency = 1.000
                Label.Size = UDim2.new(0, 260, 0, 20)
                Label.Font = Enum.Font.GothamSemibold
                Label.TextColor3 = Color3.fromRGB(225, 225, 225)
                Label.TextSize = 16.000
                Label.Text = text
                Label.TextXAlignment = Enum.TextXAlignment.Left
    
                PaddingLabel.PaddingLeft = UDim.new(0,15)
                PaddingLabel.Parent = Label
                PaddingLabel.Name = "PaddingLabel"
        
                function labell:Set(newtext)
                    Label.Text = newtext
                end
    
                return labell
            end

            return main
        end
        return uitab
    end
    return Ui
end
local function loading()
	local Loading = Instance.new("ScreenGui")
	local Blur = Instance.new("Frame")
	local Main = Instance.new("Frame")
	local UICorner = Instance.new("UICorner")
	local Logo = Instance.new("ImageLabel")
	local UICorner_2 = Instance.new("UICorner")
	local Load = Instance.new("Frame")
	local UICorner_3 = Instance.new("UICorner")
	local Bar = Instance.new("Frame")
	local UICorner_4 = Instance.new("UICorner")
	local BAR1 = Instance.new("Frame")
	local UICorner_5 = Instance.new("UICorner")
	local TextLabel = Instance.new("TextLabel")
	local Top = Instance.new("Frame")
	local UICorner_6 = Instance.new("UICorner")
	local TextLabel_2 = Instance.new("TextLabel")
	local TextLabel_3 = Instance.new("TextLabel")

	--Properties:

	Loading.Name = "Loading"
	Loading.Parent = game.CoreGui
	Loading.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

	Blur.Name = "Blur"
	Blur.Parent = Loading
	Blur.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
	Blur.BackgroundTransparency = 0.500
	Blur.Size = UDim2.new(1, 0, 1, 0)

	Main.Name = "Main"
	Main.Parent = Blur
	Main.AnchorPoint = Vector2.new(0.5, 0.5)
	Main.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
	Main.ClipsDescendants = true
	Main.Position = UDim2.new(0.5, 0, 0.499241263, 0)
	Main.Size = UDim2.new(0, 500, 0, 300)

	UICorner.Parent = Main

	Logo.Name = "Logo"
	Logo.Parent = Main
	Logo.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
	Logo.Position = UDim2.new(0.400000006, 0, 0.163333327, 0)
	Logo.Size = UDim2.new(0, 100, 0, 100)
	Logo.Image = "rbxassetid://5553946656"

	UICorner_2.CornerRadius = UDim.new(0, 100)
	UICorner_2.Parent = Logo

	Load.Name = "Load"
	Load.Parent = Main
	Load.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
	Load.Position = UDim2.new(0, 15, 0, 170)
	Load.Size = UDim2.new(0, 470, 0, 115)

	UICorner_3.Parent = Load

	Bar.Name = "Bar"
	Bar.Parent = Load
	Bar.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
	Bar.Position = UDim2.new(0, 15, 0, 80)
	Bar.Size = UDim2.new(0, 440, 0, 15)

	UICorner_4.CornerRadius = UDim.new(0, 5)
	UICorner_4.Parent = Bar

	BAR1.Name = "BAR1"
	BAR1.Parent = Bar
	BAR1.BackgroundColor3 = Color3.fromRGB(255,0,0)
	BAR1.Size = UDim2.new(0, 0, 0, 15)

	UICorner_5.CornerRadius = UDim.new(0, 5)
	UICorner_5.Parent = BAR1

	TextLabel.Parent = Load
	TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	TextLabel.BackgroundTransparency = 1.000
	TextLabel.Position = UDim2.new(0.0319148935, 0, 0.173913032, 0)
	TextLabel.Size = UDim2.new(0, 440, 0, 25)
	TextLabel.Font = Enum.Font.GothamSemibold
	TextLabel.Text = "Loading"
	TextLabel.TextColor3 = Color3.fromRGB(225, 225, 225)
	TextLabel.TextSize = 16.000
	spawn(function()
		for i = 1,5 do 
			wait(0.5)
			TextLabel.Text = "Loading."
			wait(0.5) 
			TextLabel.Text = "Loading.."
			wait(0.5)
			TextLabel.Text = "Loading..."
		end
	end)

	Top.Name = "Top"
	Top.Parent = Main
	Top.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
	Top.Size = UDim2.new(0, 500, 0, 30)

	UICorner_6.Parent = Top

	TextLabel_2.Parent = Top
	TextLabel_2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	TextLabel_2.BackgroundTransparency = 1.000
	TextLabel_2.Position = UDim2.new(0.0299999993, 0, 0, 0)
	TextLabel_2.Size = UDim2.new(0, 61, 0, 30)
	TextLabel_2.Font = Enum.Font.GothamSemibold
	TextLabel_2.Text = "Kaitan"
	TextLabel_2.TextColor3 = Color3.fromRGB(225, 225, 225)
	TextLabel_2.TextSize = 17.000

	TextLabel_3.Parent = Top
	TextLabel_3.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	TextLabel_3.BackgroundTransparency = 1.000
	TextLabel_3.Position = UDim2.new(0.151999995, 0, 0, 0)
	TextLabel_3.Size = UDim2.new(0, 61, 0, 30)
	TextLabel_3.Font = Enum.Font.GothamSemibold
	TextLabel_3.Text = "HUB"
	TextLabel_3.TextColor3 = Color3.fromRGB(255,0,0)
	TextLabel_3.TextSize = 17.000
	TextLabel_3.TextXAlignment = Enum.TextXAlignment.Left
	
	BAR1:TweenSize(UDim2.new(0,440,0,15),"Out","Linear",5,true)
	wait(5)
    Main:TweenSize(UDim2.new(0,0,0,0),"Out","Quad",0.4,true)
    wait(0.4)
	
	do 
		local Load = game.CoreGui:FindFirstChild("Loading")
		if Load then
			Load:Destroy()
		end
	end
end
loading()

if string.lower(game:GetService("RbxAnalyticsService"):GetClientId()) == game:GetService("RbxAnalyticsService"):GetClientId() then
    local ScreenGui = Instance.new("ScreenGui")
    local ImageButton = Instance.new("ImageButton")

    ScreenGui.Parent = game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui")

    ImageButton.Parent = ScreenGui
    ImageButton.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
    ImageButton.Position = UDim2.new(0.120833337, 0, 0.0952890813, 0)
    ImageButton.Size = UDim2.new(0, 50, 0, 50)
    ImageButton.Image = "rbxassetid://5553946656"
    ImageButton.MouseButton1Down:connect(function()
        game:GetService("VirtualInputManager"):SendKeyEvent(true,305,false,game)
        game:GetService("VirtualInputManager"):SendKeyEvent(false,305,false,game)
    end)
end

local win = library:AddWindow("Kaitan Hub")

local MainTab = win:AddTab("Main")
local Main1 = MainTab:AddPage()
local Main2 = MainTab:AddPage()

Main1:AddSeperator("Welcome to Kaitan")

Main1:AddLabel("Game :BF")

local timelabel = Main1:AddLabel("Server Time")

spawn(function()
    while Wait() do 
        pcall(function()
            local GameTime = math.floor(workspace.DistributedGameTime+0.5)
            local Hour = math.floor(GameTime/(60^2))%24
            local Minute = math.floor(GameTime/(60^1))%60
            local Second = math.floor(GameTime/(60^0))%60
            timelabel:Set("Server Time : "..Hour.."h "..Minute.."m "..Second.."s")
        end)
    end
end)

Main1:AddLabel("By KOBEN เป็นคนไทยทำ")

Main1:AddSeperator("Main")

Main2:AddToggle("เริ่มไก่ตัน",Config,function(value)
        AutoFarmLevel = value
end)
function InMyNetWork(object)
    if isnetworkowner then
        return isnetworkowner(object)
            else
                if (object.Position - ply.Character.HumanoidRootPart.Position).Magnitude <= 200 then 
                return true
            end
        return false
    end
end

spawn(function()
    while wait() do
        pcall(function()
            if AutoFarmLevel then
                if game:GetService("Players")["LocalPlayer"].Data.Points.Value ~= 0 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint","Melee",3)
                end
            end
        end)
    end
end)
AutoSaber=true
AutoBartilo=true
_G.SelectWeapon="Melee"
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local LocalPlayer = game:GetService("Players").LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local ply = game.Players.LocalPlayer
local placeId = game.PlaceId
if placeId == 2753915549 then
    OldWorld = true
elseif placeId == 4442272183 then
    NewWorld =  true
elseif placeId == 7449423635 then
    ThirdWorld =  true
end

pcall(function()
    if syn_crypt_encrypt then
        setfflag("HumanoidParallelRemoveNoPhysics","False")
        setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2","False")
    end  
end)

spawn(function()
    while task.wait() do
        pcall(function()
            if AutoFarmLevel then
                if AutoFarmLevel and StartMagnet then
                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                        if InMyNetWork(v.HumanoidRootPart) and (v.HumanoidRootPart.Position - PosMon.Position).Magnitude <= 200 and v.Name ~= "Greybeard [Lv. 750] [Boss]" and v.Name ~= "Ice Admiral [Lv. 700] [Boss]" and v.Name ~= "Don Swan [Lv. 3000] [Boss]" and v.Name ~= "Saber Expert [Lv. 200] [Boss]" and v.Name ~= "Longma [Lv. 2000] [Boss]" and v.Name ~= "Wysper [Lv. 500] [Boss]"  then
                            v.HumanoidRootPart.CFrame = PosMon
                            v.Humanoid.JumpPower = 0
                            v.Humanoid.WalkSpeed = 0
                            v.HumanoidRootPart.Size=Vector3.new(60,60,60)
                            v.HumanoidRootPart.CanCollide = false
                            v.Humanoid:ChangeState(11)
                            sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
                        end
                    end
                end
            end
        end)
    end
end)

task.spawn(function()
    while task.wait() do
        pcall(function()
            if AutoBartilo then
                if AutoBartilo and AutoBartiloBring then
                    if v.Name == "Swan Pirate [Lv. 775]" and (v.HumanoidRootPart.Position - PosMonBarto.Position).Magnitude <= 200 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                        v.Humanoid.JumpPower = 0
                        v.Humanoid.WalkSpeed = 0
                        v.HumanoidRootPart.CanCollide = false
                        v.HumanoidRootPart.Size=Vector3.new(60,60,60)
                        v.Humanoid:ChangeState(11)
                        v.HumanoidRootPart.CFrame = PosMonBarto
                        sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                    end
                end
            end
        end)
    end
end)

task.spawn(function()
    while task.wait() do
        if AutoFarmLevel and OldWorld and game.Players.LocalPlayer.Data.Level.Value>=100 or game.Players.LocalPlayer.Data.Level.Value>=110 then
            pcall(function()
                if ply.PlayerGui.Main.Quest.Visible == false then
                task.wait()
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("PlayerHunter")
                task.wait(.2)
                elseif ply.PlayerGui.Main.Quest.Visible == true then
                    for i,v in pairs(game:GetService("Players"):GetChildren()) do
                        if game:GetService("Players"):FindFirstChild(v.Name) then
                            if "Defeat "..v.Name.." (0/1)"==game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.text then
                                repeat task.wait()
                                    busohaki()
                                    equip(_G.SelectWeapon)
                                    keydown("T")
                                    keydown("Y")
                                    task.spawn(function()
                                        while task.wait() do
                                            if AutoFarmLevel then
                                                if game:GetService("Players")[v.Name].PlayerGui.Main.SafeZone.Visible==true then
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                                                elseif game:GetService("Players")[v.Name].PlayerGui.Main.PvpDisabled.Visible==true then
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                                                elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.PvpDisabled.Visible==true then
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EnablePvp")
                                                end
                                            end
                                        end
                                    end)
                                    task.spawn(function()
                                        while task.wait() do
                                            if AutoFarmLevel then
                                                if (game:GetService("Players")[v.Name].Character.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 10 then
                                                    keydown("Z")
                                                    task.wait(.2)
                                                    keydown("X")
                                                    task.wait(.2)
                                                    keydown("C")
                                                    task.wait(.2)
                                                    keydown("V")
                                                end
                                            end
                                        end
                                    end)
                                    spawn(function()
                                        if posrandom <= 1 then
                                            Tween(game:GetService("Players")[v.Name].Character.HumanoidRootPart.CFrame * CFrame.new(0,Distance_Farm,5))
                                            posrandom = posrandom + 0.1
                                            UesFast=false
                                        elseif posrandom >= 1 and posrandom <= 2 then
                                            Tween(game:GetService("Players")[v.Name].Character.HumanoidRootPart.CFrame * CFrame.new(5,Distance_Farm,0))
                                            posrandom = posrandom + 0.1
                                            UesFast=true
                                        elseif posrandom >= 2 and posrandom <= 3 then
                                            Tween(game:GetService("Players")[v.Name].Character.HumanoidRootPart.CFrame *CFrame.new(0,Distance_Farm,-5))
                                            posrandom = posrandom + 0.1
                                            UesFast=false
                                        elseif posrandom >= 3 and posrandom <= 4  then
                                            Tween(game:GetService("Players")[v.Name].Character.HumanoidRootPart.CFrame * CFrame.new(-5,Distance_Farm,0))
                                            posrandom = posrandom + 0.1
                                            UesFast=true
                                        elseif posrandom >=4 and posrandom <= 5 then
                                            Tween(game:GetService("Players")[v.Name].Character.HumanoidRootPart.CFrame * CFrame.new(0,5,0))
                                            posrandom = 0
                                            UesFast=false
                                        end
                                    end)
                                until not AutoFarmLevel==false or v.Humanoid.Health <= 0
                            end
                        else
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-12547.3671875, 337.1940612792969, -7565.38671875))
                        end
                    end
                end
            end)
        end
    end
end)

spawn(function()
    while wait() do
        if AutoSaber and OldWorld and game.Players.LocalPlayer.Data.Level.Value>=200 then
            AutoFarmLevel=false
            if AutoSaber and (CFrame.new(-1421.6824951171875, 48.252071380615234, 21.318946838378906).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
                bypasstp(CFrame.new(-1421.6824951171875, 48.252071380615234, 21.318946838378906))
            end
            pcall(function()
                if game:GetService("Workspace").Map.Jungle.Final:FindFirstChild("Part").Transparency == 0 then
                    TP(CFrame.new(-1421.6824951171875, 48.252071380615234, 21.318946838378906))
                    wait(.5)
                    TP(CFrame.new(-1181.1640625, 22.34051513671875, 188.13186645507812))
                    wait(.5)
                    TP(CFrame.new(-1648.1024169921875, 23.252126693725586, 438.4625549316406))
                    wait(.5)
                    TP(CFrame.new(-1153.3184814453125, 2.464047908782959, -701.0916748046875))
                    wait(.5)
                    TP(CFrame.new(-1325.6697998046875, 34.64987564086914, -463.0443420410156))
                    wait(.7)
                    TP(CFrame.new(-1610.5228271484375, 12.052069664001465, 162.6676025390625))
                    wait(.6)
                    equip("Torch")
                    wait(.5)
                    TP(CFrame.new(1115.79688, 4.92147732, 4350.17334, -0.639640629, -4.97708896e-09, 0.768674076, -2.51370613e-09, 1, 4.38315872e-09, -0.768674076, 8.71425709e-10, -0.639640629))
                    wait(6.5)
                    TP(CFrame.new(1113.51929, 5.50669432, 4365.20752, -0.821950078, -4.84191531e-08, -0.569559574, 1.90744176e-09, 1, -8.77642634e-08, 0.569559574, -7.32242427e-08, -0.821950078))
                    wait(.5)
                    equip("Cup")
                    wait(.8)
                    TP(CFrame.new(1392.83411, 37.3479347, -1323.19702, -0.0098256059, -1.19435768e-07, -0.99995172, 1.04197984e-08, 1, -1.19543927e-07, 0.99995172, -1.15938867e-08, -0.0098256059))
                    wait(5)
                    TP(CFrame.new(1458.23046875, 88.25215911865234, -1389.040283203125))
                    wait(1.2)
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","SickMan")
                    wait(.6)
                    TP(CFrame.new(-908.8209838867188, 13.752044677734375, 4078.2666015625))
                    wait(1.2)
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon")
                    wait(.5)
                    TP(CFrame.new(-2850.20068, 7.39224768, 5354.99268))
                    wait(1)
                    if game:GetService("Workspace").Enemies:FindFirstChild("Mob Leader [Lv. 120] [Boss]") then
                        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                            if v.Name == "Mob Leader [Lv. 120] [Boss]" then
                                if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                    repeat task.wait()
                                        busohaki()
                                        if v.Humanoid.Health<=0 then
                                        unequip(_G.SelectWeapon)
                                        else
                                        equip(_G.SelectWeapon)
                                        end
                                        v.HumanoidRootPart.CanCollide = false
                                        v.Humanoid.WalkSpeed = 0
                                        spawn(function()
                                            if posrandom <= 1 then
                                                Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,Distance_Farm,50))
                                                posrandom = posrandom + 0.1
                                                UesFast=false
                                            elseif posrandom >= 1 and posrandom <= 2 then
                                                Tween(v.HumanoidRootPart.CFrame * CFrame.new(50,Distance_Farm,0))
                                                posrandom = posrandom + 0.1
                                                UesFast=true
                                            elseif posrandom >= 2 and posrandom <= 3 then
                                                Tween(v.HumanoidRootPart.CFrame *CFrame.new(0,Distance_Farm,-50))
                                                posrandom = posrandom + 0.1
                                                UesFast=false
                                            elseif posrandom >= 3 and posrandom <= 4  then
                                                Tween(v.HumanoidRootPart.CFrame * CFrame.new(-50,Distance_Farm,0))
                                                posrandom = posrandom + 0.1
                                                UesFast=true
                                            elseif posrandom >=4 and posrandom <= 5 then
                                                Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
                                                posrandom = 0
                                                UesFast=false
                                            end
                                        end)
                                        sethiddenproperty(game.Players.LocalPlayer,"SimulationRadius",math.huge)
                                    until not AutoSaber or v.Humanoid.Health <= 0
                                end
                            end
                        end
                    end
                    wait(.6)
                    TP(CFrame.new(-908.8209838867188, 13.752044677734375, 4078.2666015625))
                    wait(1.2)
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon")
                    wait(1.1)
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress")
                    wait(.5)
                    equip("Relic")
                    TP(CFrame.new(-1405.82397, 29.8520069, 5.05986547, 0.759286761, 4.36840342e-09, 0.65075618, 9.78191306e-09, 1, -1.81261139e-08, -0.65075618, 2.01285584e-08, 0.759286761))
                    wait(1)
                else
                    if game:GetService("Workspace").Enemies:FindFirstChild("Saber Expert [Lv. 200] [Boss]") then
                        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                            if v.Name == "Saber Expert [Lv. 200] [Boss]" then
                                if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                    repeat task.wait()
                                        busohaki()
                                        if v.Humanoid.Health<=0 then
                                        unequip(_G.SelectWeapon)
                                        else
                                        equip(_G.SelectWeapon)
                                        end
                                        v.HumanoidRootPart.CanCollide = false
                                        v.Humanoid.WalkSpeed = 0
                                        spawn(function()
                                            if posrandom <= 1 then
                                                Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,Distance_Farm,50))
                                                posrandom = posrandom + 0.1
                                                UesFast=false
                                            elseif posrandom >= 1 and posrandom <= 2 then
                                                Tween(v.HumanoidRootPart.CFrame * CFrame.new(50,Distance_Farm,0))
                                                posrandom = posrandom + 0.1
                                                UesFast=true
                                            elseif posrandom >= 2 and posrandom <= 3 then
                                                Tween(v.HumanoidRootPart.CFrame *CFrame.new(0,Distance_Farm,-50))
                                                posrandom = posrandom + 0.1
                                                UesFast=false
                                            elseif posrandom >= 3 and posrandom <= 4  then
                                                Tween(v.HumanoidRootPart.CFrame * CFrame.new(-50,Distance_Farm,0))
                                                posrandom = posrandom + 0.1
                                                UesFast=true
                                            elseif posrandom >=4 and posrandom <= 5 then
                                                Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
                                                posrandom = 0
                                                UesFast=false
                                            end
                                        end)
                                        sethiddenproperty(game.Players.LocalPlayer,"SimulationRadius",math.huge)
                                    until not AutoSaber or not v.Parent or v.Humanoid.Health <= 0
                                end
                            end
                        end
                    else
                        if game:GetService("ReplicatedStorage"):FindFirstChild("Saber Expert [Lv. 200] [Boss]") then
                            Tween(game:GetService("ReplicatedStorage"):FindFirstChild("Saber Expert [Lv. 200] [Boss]").HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                        else
                            AutoFarmLevel=true
                        end
                    end
                end
            end)
        end
    end
end)
task.spawn(function()
    pcall(function()
        while task.wait() do
            if AutoBartilo and NewWorld and game.Players.LocalPlayer.Data.Level.Value>=850 then
                AutoFarmLevel=false
                if game:GetService("Players").LocalPlayer.Data.Level.Value >= 850 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 0 then
                    if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Swan Pirates") and string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "50") and game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then 
                        if game:GetService("Workspace").Enemies:FindFirstChild("Swan Pirate [Lv. 775]") then
                            Ms = "Swan Pirate [Lv. 775]"
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if v.Name == Ms then
                                    pcall(function()
                                        repeat task.wait()
                                            sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                                            if v.Humanoid.Health<=0 then
                                            unequip(_G.SelectWeapon)
                                            UesFast=false
                                            else
                                            equip(_G.SelectWeapon)
                                            UesFast=true
                                            end
                                            busohaki()
                                            v.HumanoidRootPart.CanCollide = false
                                            spawn(function()
                                                if posrandom <= 1 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,Distance_Farm,50))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=false
                                                elseif posrandom >= 1 and posrandom <= 2 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(50,Distance_Farm,0))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=true
                                                elseif posrandom >= 2 and posrandom <= 3 then
                                                    Tween(v.HumanoidRootPart.CFrame *CFrame.new(0,Distance_Farm,-50))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=false
                                                elseif posrandom >= 3 and posrandom <= 4  then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(-50,Distance_Farm,0))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=true
                                                elseif posrandom >=4 and posrandom <= 5 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
                                                    posrandom = 0
                                                    UesFast=false
                                                end
                                            end)												
                                            PosMonBarto =  v.HumanoidRootPart.CFrame
                                            AutoBartiloBring = true
                                        until not v.Parent or v.Humanoid.Health <= 0 or AutoBartilo == false or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
                                        AutoBartiloBring = false
                                    end)
                                end
                            end
                        else
                            TP(CFrame.new(932.624451, 156.106079, 1180.27466, -0.973085582, 4.55137119e-08, -0.230443969, 2.67024713e-08, 1, 8.47491108e-08, 0.230443969, 7.63147128e-08, -0.973085582))
                        end
                    else
                        TP(CFrame.new(-456.28952, 73.0200958, 299.895966))
                        task.wait(1.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest","BartiloQuest",1)
                    end
                elseif game:GetService("Players").LocalPlayer.Data.Level.Value >= 800 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 1 then
                    if game:GetService("Workspace").Enemies:FindFirstChild("Jeremy [Lv. 850] [Boss]") then
                        Ms = "Jeremy [Lv. 850] [Boss]"
                        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                            if v.Name == Ms then
                                repeat task.wait()
                                    sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                                    if v.Humanoid.Health<=0 then
                                    unequip(_G.SelectWeapon)
                                    else
                                    equip(_G.SelectWeapon)
                                    end
                                    busohaki()
                                    v.HumanoidRootPart.CanCollide = false
                                    spawn(function()
                                        if posrandom <= 1 then
                                            Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,Distance_Farm,50))
                                            posrandom = posrandom + 0.1
                                            UesFast=false
                                        elseif posrandom >= 1 and posrandom <= 2 then
                                            Tween(v.HumanoidRootPart.CFrame * CFrame.new(50,Distance_Farm,0))
                                            posrandom = posrandom + 0.1
                                            UesFast=true
                                        elseif posrandom >= 2 and posrandom <= 3 then
                                            Tween(v.HumanoidRootPart.CFrame *CFrame.new(0,Distance_Farm,-50))
                                            posrandom = posrandom + 0.1
                                            UesFast=false
                                        elseif posrandom >= 3 and posrandom <= 4  then
                                            Tween(v.HumanoidRootPart.CFrame * CFrame.new(-50,Distance_Farm,0))
                                            posrandom = posrandom + 0.1
                                            UesFast=true
                                        elseif posrandom >=4 and posrandom <= 5 then
                                            Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
                                            posrandom = 0
                                            UesFast=false
                                        end
                                    end)	
                                    sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
                                until not v.Parent or v.Humanoid.Health <= 0 or AutoBartilo == false
                            end
                        end
                    elseif game:GetService("ReplicatedStorage"):FindFirstChild("Jeremy [Lv. 850] [Boss]") then
                        TP(CFrame.new(-456.28952, 73.0200958, 299.895966))
                        task.wait(1.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo")
                        task.wait(1)
                        TP(CFrame.new(2099.88159, 448.931, 648.997375))
                        task.wait(2)
                    else
                        TP(CFrame.new(2099.88159, 448.931, 648.997375))
                    end
                elseif game:GetService("Players").LocalPlayer.Data.Level.Value >= 800 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 2 then
                    TP(CFrame.new(-1850.49329, 13.1789551, 1750.89685))
                    task.wait(1)
                    TP(CFrame.new(-1858.87305, 19.3777466, 1712.01807))
                    task.wait(1)
                    TP(CFrame.new(-1803.94324, 16.5789185, 1750.89685))
                    task.wait(1)
                    TP(CFrame.new(-1858.55835, 16.8604317, 1724.79541))
                    task.wait(1)
                    TP(CFrame.new(-1869.54224, 15.987854, 1681.00659))
                    task.wait(1)
                    TP(CFrame.new(-1800.0979, 16.4978027, 1684.52368))
                    task.wait(1)
                    TP(CFrame.new(-1819.26343, 14.795166, 1717.90625))
                    task.wait(1)
                    TP(CFrame.new(-1813.51843, 14.8604736, 1724.79541))
                    task.wait(10)
                    AutoFarmLevel=true
                end
            end 
        end
    end)
end)
spawn(function()
    pcall(function()
        while task.wait() do
            if AutoFarmLevel then
                function UseCode(Text)
                    game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(Text)
                end
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("kittgaming")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("Sub2Fer999")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("Enyu_is_Pro")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("JCWK")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("Starcodeheo")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("Bluxxy")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("fudd10_v2")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("FUDD10")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("BIGNEWS")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("SUB2NOOBMASTER123")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("Sub2Daigrock")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("Axiore")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("TantaiGaming")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("STRAWHATMAINE")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("3BVISITS")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("THEGREATACE")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("Bignews")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("TantaiGaming")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("SUB2GAMERROBOT_EXP1")
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer("GAMER_ROBOT_1M")
            end
        end
    end)
 end)
 local plr = game.Players.LocalPlayer
 local CbFw = debug.getupvalues(require(plr.PlayerScripts.CombatFramework))
 local CbFw2 = CbFw[2]
 function GetCurrentBlade() 
 local p13 = CbFw2.activeController
 local ret = p13.blades[1]
 if not ret then return end
 while ret.Parent~=game.Players.LocalPlayer.Character do ret=ret.Parent end
 return ret
 end
 function AttackNoCD() 
 local AC = CbFw2.activeController
 for i = 1, 1 do 
 local bladehit = require(game.ReplicatedStorage.CombatFramework.RigLib).getBladeHits(
 plr.Character,
 {plr.Character.HumanoidRootPart},
 60
 )
 local cac = {}
 local hash = {}
 for k, v in pairs(bladehit) do
 if v.Parent:FindFirstChild("HumanoidRootPart") and not hash[v.Parent] then
 table.insert(cac, v.Parent.HumanoidRootPart)
 hash[v.Parent] = true
 end
 end
 bladehit = cac
 if #bladehit > 1 then
 local u8 = debug.getupvalue(AC.attack, 5)
 local u9 = debug.getupvalue(AC.attack, 6)
 local u7 = debug.getupvalue(AC.attack, 4)
 local u10 = debug.getupvalue(AC.attack, 7)
 local u12 = (u8 * 798405 + u7 * 727595) % u9
 local u13 = u7 * 798405
 (function()
 u12 = (u12 * u9 + u13) % 1099511627776
 u8 = math.floor(u12 / u9)
 u7 = u12 - u8 * u9
 end)()
 u10 = u10 + 1
 debug.setupvalue(AC.attack, 5, u8)
 debug.setupvalue(AC.attack, 6, u9)
 debug.setupvalue(AC.attack, 4, u7)
 debug.setupvalue(AC.attack, 7, u10)
 pcall(function()
 for k, v in pairs(AC.animator.anims.basic) do
 v:Play()
 end
 end)
 if plr.Character:FindFirstChildOfClass("Tool") and AC.blades and AC.blades[1] then
 game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("weaponChange",tostring(GetCurrentBlade()))
 game.ReplicatedStorage.Remotes.Validator:FireServer(math.floor(u12 / 1099511627776 * 16777215), u10)
 game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("hit", bladehit, 1, "")
 end
 end
 end
 end
 require(game.ReplicatedStorage.Util.CameraShaker):Stop()
 task.spawn(function()
 while task.wait(math.huge) do
 pcall(function()
 if AutoFarmLevel or noclip then
 if noclip or AutoFarmLevel then
 AttackNoCD()
 end
 end
 end)
 end
 end)
task.spawn(function()
game:GetService("RunService").Stepped:Connect(function()
    if AutoFarmLevel or Noclip then 
        pcall(function()
            if syn_crypt_encrypt then 
                ply.Character.Humanoid.Sit = false
                ply.Character.Humanoid:ChangeState(11)
            else 
                ply.Character.Humanoid.Sit = false
                if not ply.Character.HumanoidRootPart:FindFirstChild("noclip") then
                    local noclip = Instance.new("BodyVelocity")
                    noclip.Name = "noclip"
                    noclip.Parent = ply.Character.HumanoidRootPart
                    noclip.MaxForce = Vector3.new(10000,10000,10000)
                    noclip.Velocity = Vector3.new(0,0,0)
                end
            end
        end)
    else 
        pcall(function()
            if ply.Character.HumanoidRootPart:FindFirstChild("noclip") then
                ply.Character.HumanoidRootPart:FindFirstChild("noclip"):Destroy()
            end
        end
        )
    end
end
)
end
)

spawn(function()
game:GetService("RunService").Stepped:Connect(function()
    if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Humanoid") then
            if syn then 
                if AutoFarmLevel or Noclip then
                    setfflag("HumanoidParallelRemoveNoPhysics", "False")
                    setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                end
            end
            for i,v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
                if v:IsA("BasePart") and v.CanCollide == true then
                     if AutoFarmLevel or Noclip then
                        v.CanCollide = false
                     else
                        v.CanCollide = true

                    end
                  end;
               end;
        end

end)
end)


function CheckQuest()
    local MyLevel = ply.Data.Level.Value
    if OldWorld then
        if MyLevel == 1 or MyLevel <= 9 or SelectMonster == "Bandit [Lv. 5]" then 
            NameMonster = "Bandit [Lv. 5]"
            QuestName = "BanditQuest1"
            LevelQuest = 1
            NameMon = "Bandit"
            CFrameQuest = CFrame.new(1061.66699, 16.5166187, 1544.52905, -0.942978859, -3.33851502e-09, 0.332852632, 7.04340497e-09, 1, 2.99841325e-08, -0.332852632, 3.06188177e-08, -0.942978859)
			if AutoFarmLevel and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetTeam",("Pirates")) 
			end
		elseif MyLevel == 10 or MyLevel <= 29 or SelectMonster == "Monkey [Lv. 14]" then 
            NameMonster = "Monkey [Lv. 14]"
            QuestName = "JungleQuest"
            LevelQuest = 1
            NameMon = "Monkey"
            CFrameQuest = CFrame.new(-1604.12012, 36.8521118, 154.23732, 0.0648873374, -4.70858913e-06, -0.997892559, 1.41431883e-07, 1, -4.70933674e-06, 0.997892559, 1.64442184e-07, 0.0648873374)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 30 or MyLevel <= 39 or SelectMonster == "Pirate [Lv. 35]" then 
            NameMonster = "Pirate [Lv. 35]"
            QuestName = "BuggyQuest1"
            LevelQuest = 1
            NameMon = "Pirate"
            CFrameQuest = CFrame.new(-1139.59717, 4.75205183, 3825.16211, -0.959730506, -7.5857054e-09, 0.280922383, -4.06310328e-08, 1, -1.11807175e-07, -0.280922383, -1.18718916e-07, -0.959730506)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 40 or MyLevel <= 59 or SelectMonster == "Brute [Lv. 45]" then 
            NameMonster = "Brute [Lv. 45]"
            QuestName = "BuggyQuest1"
            LevelQuest = 2
            NameMon = "Brute"
            CFrameQuest = CFrame.new(-1139.59717, 4.75205183, 3825.16211, -0.959730506, -7.5857054e-09, 0.280922383, -4.06310328e-08, 1, -1.11807175e-07, -0.280922383, -1.18718916e-07, -0.959730506)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 60 or MyLevel <= 74 or SelectMonster == "Desert Bandit [Lv. 60]" then 
            NameMonster = "Desert Bandit [Lv. 60]"
            QuestName = "DesertQuest"
            LevelQuest = 1
            NameMon = "Desert Bandit"
            CFrameQuest = CFrame.new(897.031128, 6.43846416, 4388.97168, -0.804044724, 3.68233266e-08, 0.594568789, 6.97835176e-08, 1, 3.24365246e-08, -0.594568789, 6.75715199e-08, -0.804044724)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 75 or MyLevel <= 89 or SelectMonster == "Desert Officer [Lv. 70]" then 
            NameMonster = "Desert Officer [Lv. 70]"
            QuestName = "DesertQuest"
            LevelQuest = 2
            NameMon = "Desert Officer"
            CFrameQuest = CFrame.new(897.031128, 6.43846416, 4388.97168, -0.804044724, 3.68233266e-08, 0.594568789, 6.97835176e-08, 1, 3.24365246e-08, -0.594568789, 6.75715199e-08, -0.804044724)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 90 or MyLevel <= 99 or SelectMonster == "Snow Bandit [Lv. 90]" then 
            NameMonster = "Snow Bandit [Lv. 90]"
            QuestName = "SnowQuest"
            LevelQuest = 1
            NameMon = "Snow Bandits"
            CFrameQuest = CFrame.new(1384.14001, 87.272789, -1297.06482, 0.348555952, -2.53947841e-09, -0.937287986, 1.49860568e-08, 1, 2.86358204e-09, 0.937287986, -1.50443711e-08, 0.348555952)
            CFrameMon = CFrame.new(1314.635498046875, 87.27279663085938, -1375.808837890625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 100 or MyLevel <= 119 or SelectMonster == "Snowman [Lv. 100]" then 
            NameMonster = "Snowman [Lv. 100]"
            QuestName = "SnowQuest"
            LevelQuest = 2
            NameMon = "Snowman"
            CFrameQuest = CFrame.new(1384.14001, 87.272789, -1297.06482, 0.348555952, -2.53947841e-09, -0.937287986, 1.49860568e-08, 1, 2.86358204e-09, 0.937287986, -1.50443711e-08, 0.348555952)
            CFrameMon = CFrame.new(1095.755859375, 105.7705078125, -1432.9976806640625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 120 or MyLevel <= 149 or SelectMonster == "Chief Petty Officer [Lv. 120]" then 
            NameMonster = "Chief Petty Officer [Lv. 120]"
            QuestName = "MarineQuest2"
            LevelQuest = 1
            NameMon = "Chief Petty Officer"
            CFrameQuest = CFrame.new(-5035.0835, 28.6520386, 4325.29443, 0.0243340395, -7.08064647e-08, 0.999703884, -6.36926814e-08, 1, 7.23777944e-08, -0.999703884, -6.54350671e-08, 0.0243340395)
            CFrameMon = CFrame.new(-4724.22314453125, 20.65203094482422, 4421.0498046875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 150 or MyLevel <= 174 or SelectMonster == "Sky Bandit [Lv. 150]" then 
            NameMonster = "Sky Bandit [Lv. 150]"
            QuestName = "SkyQuest"
            LevelQuest = 1
            NameMon = "Sky Bandit"
            CFrameQuest = CFrame.new(-4841.83447, 717.669617, -2623.96436, -0.875942111, 5.59710216e-08, -0.482416272, 3.04023082e-08, 1, 6.08195947e-08, 0.482416272, 3.86078725e-08, -0.875942111)
            CFrameMon = CFrame.new(-4956.40478515625, 365.3492736816406, -2908.31494140625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 175 or MyLevel <= 189 or SelectMonster == "Dark Master [Lv. 175]" then
            NameMonster = "Dark Master [Lv. 175]"
            LevelQuest = 2
            QuestName = "SkyQuest"
            NameMon = "Dark Master"
            CFrameQuest = CFrame.new(-4839.53027, 716.368591, -2619.44165, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
            CFrameMon = CFrame.new(-5224.42578125, 430.0478820800781, -2277.62255859375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 190 or MyLevel <= 209 or SelectMonster == "Prisoner [Lv. 190]" then
            NameMonster = "Prisoner [Lv. 190]"
            LevelQuest = 1
            QuestName = "PrisonerQuest"
            NameMon = "Prisoner"
            CFrameQuest = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
            CFrameMon = CFrame.new(5101.30224609375, 15.633732795715332, 529.2068481445312)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 210 or MyLevel <= 249 or SelectMonster == "Dangerous Prisoner [Lv. 210]" then
            NameMonster = "Dangerous Prisoner [Lv. 210]"
            LevelQuest = 2
            QuestName = "PrisonerQuest"
            NameMon = "Dangerous Prisoner"
            CFrameQuest = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
            CFrameMon = CFrame.new(5300.55029296875, 15.652962684631348, 1038.48046875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 250 or MyLevel <= 299 or SelectMonster == "Toga Warrior [Lv. 250]" then
            NameMonster = "Toga Warrior [Lv. 250]"
            LevelQuest = 1
            QuestName = "ColosseumQuest"
            NameMon = "Toga Warrior"
            CFrameQuest = CFrame.new(-1580.04663, 6.35000277, -2986.47534, -0.515037298, 0, -0.857167721, 0, 1, 0, 0.857167721, 0, -0.515037298)
            CFrameMon = CFrame.new(-1735.8134765625, 7.4425578117370605, -2780.903076171875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 300 or MyLevel <= 324 or SelectMonster == "Military Soldier [Lv. 300]" then
            NameMonster = "Military Soldier [Lv. 300]"
            LevelQuest = 1
            QuestName = "MagmaQuest"
            NameMon = "Military Soldier"
            CFrameQuest = CFrame.new(-5313.37012, 10.9500084, 8515.29395, -0.499959469, 0, 0.866048813, 0, 1, 0, -0.866048813, 0, -0.499959469)
            CFrameMon = CFrame.new(-5409.529296875, 11.032023429870605, 8460.10546875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 325 or MyLevel <= 374 or SelectMonster == "Military Spy [Lv. 325]" then
            NameMonster = "Military Spy [Lv. 325]"
            LevelQuest = 2
            QuestName = "MagmaQuest"
            NameMon = "Military Spy"
            CFrameQuest = CFrame.new(-5313.37012, 10.9500084, 8515.29395, -0.499959469, 0, 0.866048813, 0, 1, 0, -0.866048813, 0, -0.499959469)
            CFrameMon = CFrame.new(-5781.52734375, 120.05628204345703, 8780.3408203125)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 375 or MyLevel <= 399 or SelectMonster == "Fishman Warrior [Lv. 375]" then
            NameMonster = "Fishman Warrior [Lv. 375]"
            LevelQuest = 1
            QuestName = "FishmanQuest"
            NameMon = "Fishman Warrior"
            CFrameQuest = CFrame.new(61122.65234375, 18.497442245483, 1569.3997802734)
            CFrameMon = CFrame.new(60949.1015625, 18.48283576965332, 1612.7489013671875)
            if AutoFarmLevel and (CFrameQuest.Position - ply.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163, 11, 1819))
            end
        elseif MyLevel == 400 or MyLevel <= 449 or SelectMonster == "Fishman Commando [Lv. 400]" then
            NameMonster = "Fishman Commando [Lv. 400]"
            LevelQuest = 2
            QuestName = "FishmanQuest"
            NameMon = "Fishman Commando"
            CFrameQuest = CFrame.new(61122.65234375, 18.497442245483, 1569.3997802734)
            CFrameMon = CFrame.new(61899.0234375, 18.48283576965332, 1466.29443359375)
            if AutoFarmLevel and (CFrameQuest.Position - ply.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163, 11, 1819))
            end
        elseif MyLevel == 450 or MyLevel <= 474 or SelectMonster == "God's Guard [Lv. 450]" then
            NameMonster = "God's Guard [Lv. 450]"
            LevelQuest = 1
            QuestName = "SkyExp1Quest"
            NameMon = "God's Guard"
            CFrameQuest = CFrame.new(-4721.88867, 843.874695, -1949.96643, 0.996191859, -0, -0.0871884301, 0, 1, -0, 0.0871884301, 0, 0.996191859)
            CFrameMon = CFrame.new(-4696.03564453125, 845.2769775390625, -1890.16015625)
            if AutoFarmLevel and (CFrameQuest.Position - ply.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-4607.82275, 872.54248, -1667.55688))
            end
        elseif MyLevel == 475 or MyLevel <= 524 or SelectMonster == "Shanda [Lv. 475]" then
            NameMonster = "Shanda [Lv. 475]"
            LevelQuest = 2
            QuestName = "SkyExp1Quest"
            NameMon = "Shanda"
            CFrameQuest = CFrame.new(-7859.09814, 5544.19043, -381.476196, -0.422592998, 0, 0.906319618, 0, 1, 0, -0.906319618, 0, -0.422592998)
            CFrameMon = CFrame.new(-7682.05908203125, 5567.14404296875, -495.1376647949219)
            if AutoFarmLevel and (CFrameQuest.Position - ply.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
            end
        elseif MyLevel == 525 or MyLevel <= 549 or SelectMonster == "Royal Squad [Lv. 525]" then
            NameMonster = "Royal Squad [Lv. 525]"
            LevelQuest = 1
            QuestName = "SkyExp2Quest"
            NameMon = "Royal Squad"
            CFrameQuest = CFrame.new(-7906.81592, 5634.6626, -1411.99194, 0, 0, -1, 0, 1, 0, 1, 0, 0)
            CFrameMon = CFrame.new(-7736.150390625, 5612.25146484375, -1421.65234375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 550 or MyLevel <= 624 or SelectMonster == "Royal Soldier [Lv. 550]" then
            NameMonster = "Royal Soldier [Lv. 550]"
            LevelQuest = 2
            QuestName = "SkyExp2Quest"
            NameMon = "Royal Soldier"
            CFrameQuest = CFrame.new(-7906.81592, 5634.6626, -1411.99194, 0, 0, -1, 0, 1, 0, 1, 0, 0)
            CFrameMon = CFrame.new(-7822.4033203125, 5608.88037109375, -1656.308837890625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 625 or MyLevel <= 649 or SelectMonster == "Galley Pirate [Lv. 625]" then
            NameMonster = "Galley Pirate [Lv. 625]"
            LevelQuest = 1
            QuestName = "FountainQuest"
            NameMon = "Galley Pirate"
            CFrameQuest = CFrame.new(5259.81982, 37.3500175, 4050.0293, 0.087131381, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, 0.087131381)
            CFrameMon = CFrame.new(5403.00732421875, 38.50115203857422, 4013.79150390625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 650 or SelectMonster == "Galley Captain [Lv. 650]" then
            NameMonster = "Galley Captain [Lv. 650]"
            LevelQuest = 2
            QuestName = "FountainQuest"
            NameMon = "Galley Captain"
            CFrameQuest = CFrame.new(5259.81982, 37.3500175, 4050.0293, 0.087131381, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, 0.087131381)
            CFrameMon = CFrame.new(5840.06103515625, 60.19191360473633, 4892.00634765625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        end
    end
    if NewWorld then
        if MyLevel == 700 or MyLevel <= 724 or SelectMonster == "Raider [Lv. 700]" then 
            NameMonster = "Raider [Lv. 700]"
            QuestName = "Area1Quest"
            LevelQuest = 1
            NameMon = "Raider"
            CFrameQuest = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601, -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
            CFrameMon = CFrame.new(-746.3547973632812, 39.139808654785156, 2353.9951171875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 725 or MyLevel <= 774 or SelectMonster == "Mercenary [Lv. 725]" then 
            NameMonster = "Mercenary [Lv. 725]"
            QuestName = "Area1Quest"
            LevelQuest = 2
            NameMon = "Mercenary"
            CFrameQuest = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601, -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
            CFrameMon = CFrame.new(-978.2632446289062, 73.00972747802734, 1437.860595703125)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 775 or MyLevel <= 874 or SelectMonster == "Swan Pirate [Lv. 775]" then 
            NameMonster = "Swan Pirate [Lv. 775]"
            QuestName = "Area2Quest"
            LevelQuest = 1
            NameMon = "Swan Pirate"
            CFrameQuest = CFrame.new(632.698608, 73.1055908, 918.666321, -0.0319722369, 8.96074881e-10, -0.999488771, 1.36326533e-10, 1, 8.92172336e-10, 0.999488771, -1.07732087e-10, -0.0319722369)
            CFrameMon = CFrame.new(896.3140869140625, 72.95972442626953, 1273.1866455078125)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 875 or MyLevel <= 899 or SelectMonster == "Marine Lieutenant [Lv. 875]" then 
            NameMonster = "Marine Lieutenant [Lv. 875]"
            QuestName = "MarineQuest3"
            LevelQuest = 1
            NameMon = "Marine Lieutenant"
            CFrameQuest = CFrame.new(-2442.65015, 73.0511475, -3219.11523, -0.873540044, 4.2329841e-08, -0.486752301, 5.64383384e-08, 1, -1.43220786e-08, 0.486752301, -3.99823996e-08, -0.873540044)
            CFrameMon = CFrame.new(-2736.815185546875, 72.84119415283203, -3046.572509765625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 900 or MyLevel <= 949 or SelectMonster == "Marine Captain [Lv. 900]" then 
            NameMonster = "Marine Captain [Lv. 900]"
            QuestName = "MarineQuest3"
            LevelQuest = 2
            NameMon = "Marine Captain"
            CFrameQuest = CFrame.new(-2442.65015, 73.0511475, -3219.11523, -0.873540044, 4.2329841e-08, -0.486752301, 5.64383384e-08, 1, -1.43220786e-08, 0.486752301, -3.99823996e-08, -0.873540044)
            CFrameMon = CFrame.new(-1993.48779296875, 72.96614837646484, -3228.642578125)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 950 or MyLevel <= 974 or SelectMonster == "Zombie [Lv. 950]" then 
            NameMonster = "Zombie [Lv. 950]"
            QuestName = "ZombieQuest"
            LevelQuest = 1
            NameMon = "Zombie"
            CFrameQuest = CFrame.new(-5492.79395, 48.5151672, -793.710571, 0.321800292, -6.24695815e-08, 0.946807742, 4.05616092e-08, 1, 5.21931227e-08, -0.946807742, 2.16082796e-08, 0.321800292)
            CFrameMon = CFrame.new(-5542.67041015625, 48.48012924194336, -879.48388671875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 975 or MyLevel <= 999 or SelectMonster == "Vampire [Lv. 975]" then 
            NameMonster = "Vampire [Lv. 975]"
            QuestName = "ZombieQuest"
            LevelQuest = 2
            NameMon = "Vampire"
            CFrameQuest = CFrame.new(-5492.79395, 48.5151672, -793.710571, 0.321800292, -6.24695815e-08, 0.946807742, 4.05616092e-08, 1, 5.21931227e-08, -0.946807742, 2.16082796e-08, 0.321800292)
            CFrameMon = CFrame.new(-5962.5810546875, 6.402710914611816, -1283.3720703125)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 1000 or MyLevel <= 1049 or SelectMonster == "Snow Trooper [Lv. 1000]" then 
            NameMonster = "Snow Trooper [Lv. 1000]"
            QuestName = "SnowMountainQuest"
            LevelQuest = 1
            NameMon = "Snow Trooper"
            CFrameQuest = CFrame.new(604.964966, 401.457062, -5371.69287, 0.353063971, 1.89520435e-08, -0.935599446, -5.81846002e-08, 1, -1.70033754e-09, 0.935599446, 5.50377841e-08, 0.353063971)
            CFrameMon = CFrame.new(518.447998046875, 401.4220275878906, -5348.09765625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 1050 or MyLevel <= 1099 or SelectMonster == "Winter Warrior [Lv. 1050]" then 
            NameMonster = "Winter Warrior [Lv. 1050]"
            QuestName = "SnowMountainQuest"
            LevelQuest = 2
            NameMon = "Winter Warrior"
            CFrameQuest = CFrame.new(604.964966, 401.457062, -5371.69287, 0.353063971, 1.89520435e-08, -0.935599446, -5.81846002e-08, 1, -1.70033754e-09, 0.935599446, 5.50377841e-08, 0.353063971)
            CFrameMon = CFrame.new(1302.9853515625, 429.4219665527344, -5284.79931640625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 1100 or MyLevel <= 1124 or SelectMonster == "Lab Subordinate [Lv. 1100]" then 
            NameMonster = "Lab Subordinate [Lv. 1100]"
            QuestName = "IceSideQuest"
            LevelQuest = 1
            NameMon = "Lab Subordinate"
            CFrameQuest = CFrame.new(-6060.10693, 15.9868021, -4904.7876, -0.411000341, -5.06538868e-07, 0.91163528, 1.26306062e-07, 1, 6.12581289e-07, -0.91163528, 3.66916197e-07, -0.411000341)
            CFrameMon = CFrame.new(-5826.08984375, 15.951773643493652, -4418.52099609375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 1125 or MyLevel <= 1174 or SelectMonster == "Horned Warrior [Lv. 1125]" then 
            NameMonster = "Horned Warrior [Lv. 1125]"
            QuestName = "IceSideQuest"
            LevelQuest = 2
            NameMon = "Horned Warrior"
            CFrameQuest = CFrame.new(-6060.10693, 15.9868021, -4904.7876, -0.411000341, -5.06538868e-07, 0.91163528, 1.26306062e-07, 1, 6.12581289e-07, -0.91163528, 3.66916197e-07, -0.411000341)
            CFrameMon = CFrame.new(-6287.04296875, 17.54484748840332, -5854.72802734375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 1175 or MyLevel <= 1199 or SelectMonster == "Magma Ninja [Lv. 1175]" then 
            NameMonster = "Magma Ninja [Lv. 1175]"
            QuestName = "FireSideQuest"
            LevelQuest = 1
            NameMon = "Magma Ninja"
            CFrameQuest = CFrame.new(-5431.09473, 15.9868021, -5296.53223, 0.831796765, 1.15322464e-07, -0.555080295, -1.10814341e-07, 1, 4.17010995e-08, 0.555080295, 2.68240168e-08, 0.831796765)
            CFrameMon = CFrame.new(-5698.142578125, 15.951773643493652, -5786.8271484375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 1200 or MyLevel <= 1249 or SelectMonster == "Lava Pirate [Lv. 1200]" then 
            NameMonster = "Lava Pirate [Lv. 1200]"
            QuestName = "FireSideQuest"
            LevelQuest = 2
            NameMon = "Lava Pirate"
            CFrameQuest = CFrame.new(-5431.09473, 15.9868021, -5296.53223, 0.831796765, 1.15322464e-07, -0.555080295, -1.10814341e-07, 1, 4.17010995e-08, 0.555080295, 2.68240168e-08, 0.831796765)
            CFrameMon = CFrame.new(-5346.04638671875, 15.951773643493652, -4740.6533203125)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 1250 or MyLevel <= 1274 or SelectMonster == "Ship Deckhand [Lv. 1250]" then 
            NameMonster = "Ship Deckhand [Lv. 1250]"
            QuestName = "ShipQuest1"
            LevelQuest = 1
            NameMon = "Ship Deckhand"
            CFrameQuest = CFrame.new(1037.80127, 125.092171, 32911.6016, -0.244533166, -0, -0.969640911, -0, 1.00000012, -0, 0.96964103, 0, -0.244533136)
            CFrameMon = CFrame.new(1182.887939453125, 125.7291488647461, 32988.875)
            if AutoFarmLevel and (CFrameMon.Position - ply.Character.HumanoidRootPart.Position).Magnitude > 20000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
            end
        elseif MyLevel == 1275 or MyLevel <= 1299 or SelectMonster == "Ship Engineer [Lv. 1275]" then 
            NameMonster = "Ship Engineer [Lv. 1275]"
            QuestName = "ShipQuest1"
            LevelQuest = 2
            NameMon = "Ship Engineer"
            CFrameQuest = CFrame.new(1037.80127, 125.092171, 32911.6016, -0.244533166, -0, -0.969640911, -0, 1.00000012, -0, 0.96964103, 0, -0.244533136)
            CFrameMon = CFrame.new(954.09716796875, 40.05690383911133, 32709.890625)
            if AutoFarmLevel and (CFrameMon.Position - ply.Character.HumanoidRootPart.Position).Magnitude > 20000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
            end
        elseif MyLevel == 1300 or MyLevel <= 1324 or SelectMonster == "Ship Steward [Lv. 1300]" then 
            NameMonster = "Ship Steward [Lv. 1300]"
            QuestName = "ShipQuest2"
            LevelQuest = 1
            NameMon = "Ship Steward"
            CFrameQuest = CFrame.new(968.80957, 125.092171, 33244.125, -0.869560242, 1.51905191e-08, -0.493826836, 1.44108379e-08, 1, 5.38534195e-09, 0.493826836, -2.43357912e-09, -0.869560242)
            CFrameMon = CFrame.new(969.2874145507812, 125.18672943115234, 33448.76171875)
            if AutoFarmLevel and (CFrameMon.Position - ply.Character.HumanoidRootPart.Position).Magnitude > 20000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
            end
        elseif MyLevel == 1325 or MyLevel <= 1349 or SelectMonster == "Ship Officer [Lv. 1325]" then 
            NameMonster = "Ship Officer [Lv. 1325]"
            QuestName = "ShipQuest2"
            LevelQuest = 2
            NameMon = "Ship Officer"
            CFrameQuest = CFrame.new(968.80957, 125.092171, 33244.125, -0.869560242, 1.51905191e-08, -0.493826836, 1.44108379e-08, 1, 5.38534195e-09, 0.493826836, -2.43357912e-09, -0.869560242)
            CFrameMon = CFrame.new(1243.881103515625, 181.05767822265625, 33426.046875)
            if AutoFarmLevel and (CFrameMon.Position - ply.Character.HumanoidRootPart.Position).Magnitude > 20000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
            end
        elseif MyLevel == 1350 or MyLevel <= 1374 or SelectMonster == "Arctic Warrior [Lv. 1350]" then 
            NameMonster = "Arctic Warrior [Lv. 1350]"
            QuestName = "FrostQuest"
            LevelQuest = 1
            NameMon = "Arctic Warrior"
            CFrameQuest = CFrame.new(5669.43506, 28.2117786, -6482.60107, 0.888092756, 1.02705066e-07, 0.459664226, -6.20391774e-08, 1, -1.03572376e-07, -0.459664226, 6.34646895e-08, 0.888092756)
            CFrameMon = CFrame.new(6038.34765625, 28.366756439208984, -6259.73046875)
            if AutoFarmLevel and (CFrameMon.Position - ply.Character.HumanoidRootPart.Position).Magnitude > 20000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
            end
        elseif MyLevel == 1375 or MyLevel <= 1424 or SelectMonster == "Snow Lurker [Lv. 1375]" then 
            NameMonster = "Snow Lurker [Lv. 1375]"
            QuestName = "FrostQuest"
            LevelQuest = 2
            NameMon = "Snow Lurker"
            CFrameQuest = CFrame.new(5669.43506, 28.2117786, -6482.60107, 0.888092756, 1.02705066e-07, 0.459664226, -6.20391774e-08, 1, -1.03572376e-07, -0.459664226, 6.34646895e-08, 0.888092756)
            CFrameMon = CFrame.new(5595.2841796875, 28.614917755126953, -6749.4296875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 1425 or MyLevel <= 1449 or SelectMonster == "Sea Soldier [Lv. 1425]" then 
            NameMonster = "Sea Soldier [Lv. 1425]"
            QuestName = "ForgottenQuest"
            LevelQuest = 1
            NameMon = "Sea Soldier"
            CFrameQuest = CFrame.new(-3052.99097, 236.881363, -10148.1943, -0.997911751, 4.42321983e-08, 0.064591676, 4.90968759e-08, 1, 7.37270085e-08, -0.064591676, 7.67442998e-08, -0.997911751)
            CFrameMon = CFrame.new(-3355.1494140625, 26.95261001586914, -9768.0185546875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1450 or SelectMonster == "Water Fighter [Lv. 1450]" then 
            NameMonster = "Water Fighter [Lv. 1450]"
            QuestName = "ForgottenQuest"
            LevelQuest = 2
            NameMon = "Water Fighter"
            CFrameQuest = CFrame.new(-3052.99097, 236.881363, -10148.1943, -0.997911751, 4.42321983e-08, 0.064591676, 4.90968759e-08, 1, 7.37270085e-08, -0.064591676, 7.67442998e-08, -0.997911751)
            CFrameMon = CFrame.new(-3431.481201171875, 238.84617614746094, -10512.75)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        end
    end
    if ThirdWorld then
        if MyLevel >= 1500 and MyLevel <= 1524 or SelectMonster == "Pirate Millionaire [Lv. 1500]" then
            NameMonster = "Pirate Millionaire [Lv. 1500]"
            QuestName = "PiratePortQuest"
            LevelQuest = 1
            NameMon = "Pirate Millionaire"
            CFrameQuest = CFrame.new(-290.074677, 42.9034653, 5581.58984)
            CFrameMon = CFrame.new(-32.53920364379883, 43.855770111083984, 5617.40478515625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1525 and MyLevel <= 1574 or SelectMonster == "Pistol Billionaire [Lv. 1525]" then
            NameMonster = "Pistol Billionaire [Lv. 1525]"
            QuestName = "PiratePortQuest"
            LevelQuest = 2
            NameMon = "Pistol Billionaire"
            CFrameQuest = CFrame.new(-290.074677, 42.9034653, 5581.58984)
            CFrameMon = CFrame.new(-209.0025634765625, 73.83525848388672, 5973.78466796875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1575 and MyLevel <= 1599 or SelectMonster == "Dragon Crew Warrior [Lv. 1575]" then
            NameMonster = "Dragon Crew Warrior [Lv. 1575]"
            QuestName = "AmazonQuest"
            LevelQuest = 1
            NameMon = "Dragon Crew Warrior"
            CFrameQuest = CFrame.new(5832.83594, 51.6806107, -1101.51563)
            CFrameMon = CFrame.new(4286.03466796875, 51.47886657714844, -1338.9012451171875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1600 and MyLevel <= 1624 or SelectMonster == "Dragon Crew Archer [Lv. 1600]" then
            NameMonster = "Dragon Crew Archer [Lv. 1600]"
            QuestName = "AmazonQuest"
            LevelQuest = 2
            NameMon = "Dragon Crew Archer"
            CFrameQuest = CFrame.new(5832.83594, 51.6806107, -1101.51563)
            CFrameMon = CFrame.new(6673.52490234375, 378.4156188964844, 338.1069030761719)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1625 and MyLevel <= 1699 or SelectMonster == "Female Islander [Lv. 1625]" then
            NameMonster = "Female Islander [Lv. 1625]"
            QuestName = "AmazonQuest2"
            LevelQuest = 1
            NameMon = "Female Islander"
            CFrameQuest = CFrame.new(5448.86133, 601.516174, 751.130676)
            CFrameMon = CFrame.new(4769.5, 730.3597412109375, 926.3622436523438)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1700 and MyLevel <= 1724 or SelectMonster == "Marine Commodore [Lv. 1700]" then
            NameMonster = "Marine Commodore [Lv. 1700]"
            QuestName = "MarineTreeIsland"
            LevelQuest = 1
            NameMon = "Marine Commodore"
            CFrameQuest = CFrame.new(2180.54126, 27.8156815, -6741.5498)
            CFrameMon = CFrame.new(2385.248046875, 73.15121459960938, -7272.90966796875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1725 and MyLevel <= 1774 or SelectMonster == "Marine Rear Admiral [Lv. 1725]" then
            NameMonster = "Marine Rear Admiral [Lv. 1725]"
            QuestName = "MarineTreeIsland"
            LevelQuest = 2
            NameMon = "Marine Rear Admiral"
            CFrameQuest = CFrame.new(2180.54126, 27.8156815, -6741.5498)
            CFrameMon = CFrame.new(3564.876220703125, 160.54989624023438, -7144.53759765625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1775 and MyLevel <= 1799 or SelectMonster == "Fishman Raider [Lv. 1775]" then
            NameMonster = "Fishman Raider [Lv. 1775]"
            QuestName = "DeepForestIsland3"
            LevelQuest = 1
            NameMon = "Fishman Raider"
            CFrameQuest = CFrame.new(-10581.6563, 330.872955, -8761.18652)
            CFrameMon = CFrame.new(-10202.849609375, 331.78851318359375, -8329.98046875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1800 and MyLevel <= 1824 or SelectMonster == "Fishman Captain [Lv. 1800]" then
            NameMonster = "Fishman Captain [Lv. 1800]"
            QuestName = "DeepForestIsland3"
            LevelQuest = 2
            NameMon = "Fishman Captain"
            CFrameQuest = CFrame.new(-10581.6563, 330.872955, -8761.18652)
            CFrameMon = CFrame.new(-11066.0869140625, 331.74908447265625, -9167.8583984375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1825 and MyLevel <= 1899 or SelectMonster == "Forest Pirate [Lv. 1825]" then
            NameMonster = "Forest Pirate [Lv. 1825]"
            QuestName = "DeepForestIsland"
            LevelQuest = 1
            NameMon = "Forest Pirate"
            CFrameQuest = CFrame.new(-13234.04, 331.488495, -7625.40137)
            CFrameMon = CFrame.new(-13370.51953125, 332.4039306640625, -7705.765625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1900 and MyLevel <= 1924 or SelectMonster == "Jungle Pirate [Lv. 1900]" then
            NameMonster = "Jungle Pirate [Lv. 1900]"
            QuestName = "DeepForestIsland2"
            LevelQuest = 1
            NameMon = "Jungle Pirate"
            CFrameQuest = CFrame.new(-12680.3818, 389.971039, -9902.01953)
            CFrameMon = CFrame.new(-11897.876953125, 331.7640686035156, -10577.7333984375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1925 and MyLevel <= 1974 or SelectMonster == "Musketeer Pirate [Lv. 1925]" then
            NameMonster = "Musketeer Pirate [Lv. 1925]"
            QuestName = "DeepForestIsland2"
            LevelQuest = 2
            NameMon = "Musketeer Pirate"
            CFrameQuest = CFrame.new(-12680.3818, 389.971039, -9902.01953)
            CFrameMon = CFrame.new(-13396.6591796875, 391.5714416503906, -9807.1806640625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 1975 and MyLevel <= 1999 or SelectMonster == "Reborn Skeleton [Lv. 1975]" then
            NameMonster = "Reborn Skeleton [Lv. 1975]"
            QuestName = "HauntedQuest1"
            LevelQuest = 1
            NameMon = "Reborn Skeleton"
            CFrameQuest = CFrame.new(-9480.8271484375, 142.13066101074, 5566.0712890625)
            CFrameMon = CFrame.new(-8762.4326171875, 142.1306610107422, 6011.48828125)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2000 and MyLevel <= 2024 or SelectMonster == "Living Zombie [Lv. 2000]" then
            NameMonster = "Living Zombie [Lv. 2000]"
            QuestName = "HauntedQuest1"
            LevelQuest = 2
            NameMon = "Living Zombie"
            CFrameQuest = CFrame.new(-9480.8271484375, 142.13066101074, 5566.0712890625)
            CFrameMon = CFrame.new(-10150.359375, 138.6525115966797, 6019.853515625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2025 and MyLevel <= 2049 or SelectMonster == "Demonic Soul [Lv. 2025]" then
            NameMonster = "Demonic Soul [Lv. 2025]"
            QuestName = "HauntedQuest2"
            LevelQuest = 1
            NameMon = "Demonic Soul"
            CFrameQuest = CFrame.new(-9516.9931640625, 178.00651550293, 6078.4653320313)
            CFrameMon = CFrame.new(-9451.4296875, 172.1306610107422, 6152.09912109375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel > 2050 and MyLevel <= 2074 or SelectMonster == "Posessed Mummy [Lv. 2050]" then
            NameMonster = "Posessed Mummy [Lv. 2050]"
            QuestName = "HauntedQuest2"
            LevelQuest = 2
            NameMon = "Posessed Mummy"
            CFrameQuest = CFrame.new(-9516.9931640625, 178.00651550293, 6078.4653320313)
            CFrameMon = CFrame.new(-9514.3544921875, 6.130645751953125, 6300.54052734375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2075 and MyLevel <= 2099 or SelectMonster == "Peanut Scout [Lv. 2075]" then
            NameMonster = "Peanut Scout [Lv. 2075]"
            QuestName = "NutsIslandQuest"
            LevelQuest = 1
            NameMon = "Peanut Scout"
            CFrameQuest = CFrame.new(-2104.5874, 38.1299706, -10194.3496, 0.774643302, -5.8516525e-09, 0.632398427, -4.8110703e-08, 1, 6.81853152e-08, -0.632398427, -8.324443e-08, 0.774643302)
            CFrameMon = CFrame.new(-2030.8466796875, 38.129024505615234, -10052.5234375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2100 and MyLevel <= 2124 or SelectMonster == "Peanut President [Lv. 2100]" then
            NameMonster = "Peanut President [Lv. 2100]"
            QuestName = "NutsIslandQuest"
            LevelQuest = 2
            NameMon = "Peanut President"
            CFrameQuest = CFrame.new(-2104.2546386719, 38.129970550537, -10194.146484375)
            CFrameMon = CFrame.new(-2314.987548828125, 88.31883239746094, -10481.2724609375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2125 and MyLevel <= 2149 or SelectMonster == "Ice Cream Chef [Lv. 2125]" then
            NameMonster = "Ice Cream Chef [Lv. 2125]"
            QuestName = "IceCreamIslandQuest"
            LevelQuest = 1
            NameMon = "Ice Cream Chef"
            CFrameQuest = CFrame.new(-820.336182, 65.8453293, -10965.7627, 0.763408899, 2.66162115e-08, -0.645915508, 5.54280488e-09, 1, 4.77580073e-08, 0.645915508, -4.00390725e-08, 0.763408899)
            CFrameMon = CFrame.new(-1060.117431640625, 65.84529113769531, -10952.587890625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2150  and MyLevel <= 2199 or SelectMonster == "Ice Cream Commander [Lv. 2150]" then
            NameMonster = "Ice Cream Commander [Lv. 2150]"
            QuestName = "IceCreamIslandQuest"
            LevelQuest = 2
            NameMon = "Ice Cream Commander"
            CFrameQuest = CFrame.new(-820.336182, 65.8453293, -10965.7627, 0.763408899, 2.66162115e-08, -0.645915508, 5.54280488e-09, 1, 4.77580073e-08, 0.645915508, -4.00390725e-08, 0.763408899)
            CFrameMon = CFrame.new(-712.1015014648438, 65.84538269042969, -11319.521484375)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2200 and MyLevel <= 2249 or SelectMonster == "Cookie Crafter [Lv. 2200]" then
            NameMonster = "Cookie Crafter [Lv. 2200]"
            QuestName = "CakeQuest1"
            LevelQuest = 1
            NameMon = "Cookie Crafter"
            CFrameQuest = CFrame.new(-2021.96851, 37.7982178, -12026.5137, 0.971608818, 1.80562854e-08, 0.236593053, -1.95491463e-08, 1, 3.96393229e-09, -0.236593053, -8.47658388e-09, 0.971608818)
            CFrameMon = CFrame.new(-2354.45703125, 37.82392501831055, -12114.884765625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2250  and MyLevel <= 2274 or SelectMonster == "Baking Staff [Lv. 2250]" then
            NameMonster = "Baking Staff [Lv. 2250]"
            QuestName = "CakeQuest2" 
            LevelQuest = 1
            NameMon = "Baking Staff"
            CFrameQuest = CFrame.new(-1927.58313, 37.7981453, -12843.8145, -0.961271644, -8.12611574e-07, 0.275603265, -7.71673683e-07, 1, 2.56976563e-07, -0.275603265, 3.43484281e-08, -0.961271644)
            CFrameMon = CFrame.new(-1818.0260009765625, 37.823944091796875, -12860.091796875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2275 and MyLevel <= 2299 or SelectMonster == "Head Baker [Lv. 2275]" then
            NameMonster = "Head Baker [Lv. 2275]"
            QuestName = "CakeQuest2" 
            LevelQuest = 2
            NameMon = "Head Baker"
            CFrameQuest = CFrame.new(-1927.58313, 37.7981453, -12843.8145, -0.961271644, -8.12611574e-07, 0.275603265, -7.71673683e-07, 1, 2.56976563e-07, -0.275603265, 3.43484281e-08, -0.961271644)
            CFrameMon = CFrame.new(-2254.647705078125, 53.528289794921875, -12837.6025390625)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2300 and MyLevel <= 2325-1 or SelectMonster ==  "Cocoa Warrior [Lv. 2300]" then
            NameMonster = "Cocoa Warrior [Lv. 2300]"
            QuestName = "ChocQuest1"
            LevelQuest = 1
            NameMon = "Cocoa Warrior"
            CFrameQuest = CFrame.new(232.6294708251953, 30.181140899658203, -12200.2197265625)		
            CFrameMon = CFrame.new(-29.486034393310547, 24.760190963745117, -12234.4013671875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2325 and MyLevel <= 2350-1 or SelectMonster == "Chocolate Bar Battler [Lv. 2325]" then
            NameMonster = "Chocolate Bar Battler [Lv. 2325]"
            QuestName = "ChocQuest1"
            LevelQuest = 2
            NameMon = "Chocolate Bar Battler"
            CFrameQuest = CFrame.new(232.6294708251953, 30.181140899658203, -12200.2197265625)
            CFrameMon = CFrame.new(715.9921264648438, 24.760162353515625, -12640.23046875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel >= 2350 and MyLevel <= 2375-1 or SelectMonster == "Sweet Thief [Lv. 2350]" then
            NameMonster = "Sweet Thief [Lv. 2350]"
            QuestName = "ChocQuest2"
            LevelQuest = 1
            NameMon = "Sweet Thief"
            CFrameQuest = CFrame.new(149.97471618652344, 30.667919158935547, -12775.0830078125)
            CFrameMon = CFrame.new(18.782255172729492, 24.819686889648438, -12615.10546875)
            if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel == 2375 or  MyLevel <= 2400-1 or SelectMonster == "Candy Rebel [Lv. 2375]" then
            NameMonster = "Candy Rebel [Lv. 2375]"
            QuestName = "ChocQuest2"
            LevelQuest = 2
            NameMon = "Candy Rebel"
            CFrameQuest = CFrame.new(149.97471618652344, 30.667919158935547, -12775.0830078125)
            CFrameMon = CFrame.new(44.659332275390625, 24.81971549987793, -12921.310546875)	
        if AutoFarmLevel and SelectModeTween=="TweenBypass" and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
            bypasstp(CFrameQuest)
        end
        elseif MyLevel==2400 or MyLevel<=2425-1 or SelectMonster == "Candy Rebel [Lv. 2375]" then
            NameMonster = "Candy Pirate [Lv. 2400]"
            QuestName = "CandyQuest1"
            LevelQuest = 1
            NameMon = "Candy Pirate"
            CFrameQuest = CFrame.new(-1146.039794921875, 16.142284393310547, -14447.57421875)
            CFrameMon = CFrame.new(-1146.039794921875, 16.142284393310547, -14447.57421875)	
            if AutoFarmLevel and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        elseif MyLevel>=2425 or SelectMonster == "Snow Demon [Lv. 2425]" then
            NameMonster = "Snow Demon [Lv. 2425]"
            QuestName = "CandyQuest1"
            LevelQuest = 2
            NameMon = "Snow Demon"
            CFrameQuest = CFrame.new(-1146.039794921875, 16.142284393310547, -14447.57421875)
            CFrameMon = CFrame.new(-1146.039794921875, 16.142284393310547, -14447.57421875)	
            if AutoFarmLevel and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2500 then
                bypasstp(CFrameQuest)
            end
        end
    end
end
function CurrentWeapon()
    local ac = CombatFrameworkR.activeController
    local ret = ac.blades[1]
    if not ret then return ply.Character:FindFirstChildOfClass("Tool").Name end
    pcall(function()
        while ret.Parent~=ply.Character do ret=ret.Parent end
    end)
    if not ret then return ply.Character:FindFirstChildOfClass("Tool").Name end
    return ret
end

function equip(typ) --- equip tool
	for i, v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
		if(v:IsA('Tool'))then
			if(v.ToolTip==typ or v.Name==typ )then
				game.Players.LocalPlayer.Character.Humanoid:EquipTool(v)
			end
		end
	end
end


function unequip(Toolse) --- equip tool
    if game.Players.LocalPlayer.Character:FindFirstChild(Toolse) then
        _G.NotAutoEquip = true
        wait(.5)
        game.Players.LocalPlayer.Character:FindFirstChild(Toolse).Parent = game.Players.LocalPlayer.Backpack
        wait(.1)
        _G.NotAutoEquip = false
    end
end


function bypasstp(Position)
    game:service('VirtualInputManager'):SendKeyEvent(true, "W", false, game)
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
	wait(1)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
    game.Players.LocalPlayer.Character.Head:Destroy()
    game:service('VirtualInputManager'):SendKeyEvent(false, "W", false, game)
end

function busohaki()
    if not game:GetService("Players").LocalPlayer.Character:FindFirstChild("HasBuso") then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
    end
end
TPQuest=function(TP)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame=TP
end

Tween=function(Pos)
    Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
    if game.Players.LocalPlayer.Character.Humanoid.Sit == true then game.Players.LocalPlayer.Character.Humanoid.Sit = false end
    pcall(function() tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/60, Enum.EasingStyle.Quint),{CFrame = Pos}) end)--Quint
    tween:Play()
    if _G.StopTween == true then
        tween:Cancel()
        _G.Clip = false
    end
end

function GetDistance(target)
    return math.floor((target.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude)
end

function TP(Pos)
    repeat wait()
        Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
        if game.Players.LocalPlayer.Character.Humanoid.Sit == true then game.Players.LocalPlayer.Character.Humanoid.Sit = false end
        pcall(function() tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/150, Enum.EasingStyle.Linear),{CFrame = Pos}) end)
        tween:Play()
        if Distance <= 150 then
            tween:Cancel()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
        end
        if _G.StopTween == true then
            tween:Cancel()
            _G.Clip = false
        end
    until Distance <= 80
end

task.spawn(function()
    while task.wait() do
        if AutoFarmLevel then
            _G.rejoin = game:GetService("CoreGui").RobloxPromptGui.promptOverlay.ChildAdded:Connect(function(Kick)
                if not _G.Rejoin then
                    if Kick.Name == 'ErrorPrompt' and Kick:FindFirstChild('MessageArea') and Kick.MessageArea:FindFirstChild("ErrorFrame") then
                        game:GetService("TeleportService"):Teleport(game.PlaceId)
                        task.wait(1)
                    end
                end
            end)
        end
    end
end)

posrandom = 0

task.spawn(function()
    while wait() do
        if AutoFarmLevel then
            if ply.Data.Level.Value >= 30 and ply.Data.Level.Value <= 100 then
                if (CFrame.new(-7894, 5547, -380).Position - ply.Character.HumanoidRootPart.Position).Magnitude <= 3500 then
                    repeat wait()
                        pcall(function()
                            if game:GetService("Workspace").Enemies:FindFirstChild("Royal Squad [Lv. 525]") then
                                for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                    if v.Name == "Royal Squad [Lv. 525]" and v.Humanoid.Health ~= 0 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") then
                                        repeat task.wait()
                                            StartMagnet = true
                                            PosMon = v.HumanoidRootPart.CFrame
                                            if v.Humanoid.Health <= 0 then
                                                unequip(_G.SelectWeapon)
                                            else
                                                equip(_G.SelectWeapon)
                                            end
                                            spawn(function()
                                                if posrandom <= 1 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,Distance_Farm,50))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=false
                                                elseif posrandom >= 1 and posrandom <= 2 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(50,Distance_Farm,0))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=true
                                                elseif posrandom >= 2 and posrandom <= 3 then
                                                    Tween(v.HumanoidRootPart.CFrame *CFrame.new(0,Distance_Farm,-50))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=false
                                                elseif posrandom >= 3 and posrandom <= 4  then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(-50,Distance_Farm,0))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=true
                                                elseif posrandom >=4 and posrandom <= 5 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
                                                    posrandom = 0
                                                    UesFast=false
                                                end
                                            end)				
                                            if AutoFarmLevel then
                                                if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 150 then
                                                    game:service('VirtualInputManager'):SendKeyEvent(true, "V", false, game)
                                                    game:service('VirtualInputManager'):SendKeyEvent(false, "V", false, game)
											    end
                                            end
                                            busohaki()
                                            v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                            v.Humanoid.JumpPower = 0
                                            v.Humanoid.WalkSpeed = 0
                                            v.HumanoidRootPart.CanCollide = false
                                            if v.Humanoid:FindFirstChild("Animator") then
                                                v.Humanoid.Animator:Destroy()
                                            end
                                            v.Humanoid:ChangeState(11)
                                            sethiddenproperty(ply, "SimulationRadius",  math.huge)
                                        until not AutoFarmLevel or v.Humanoid.Health <= 0
                                    end
                                end
                            elseif game:GetService("ReplicatedStorage"):FindFirstChild("Royal Squad [Lv. 525]") then
                                Tween(game:GetService("ReplicatedStorage"):FindFirstChild("Royal Squad [Lv. 525]").HumanoidRootPart.CFrame * CFrame.new(0,20,0))
                            elseif game:GetService("Workspace").Enemies:FindFirstChild("Shanda [Lv. 475]") then
                                for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                    if v.Name == "Shanda [Lv. 475]" and v.Humanoid.Health ~= 0 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") then
                                        repeat task.wait()
                                            StartMagnet = true
                                            PosMon = v.HumanoidRootPart.CFrame
                                            if v.Humanoid.Health <= 0 then
                                                unequip(_G.SelectWeapon)
                                            else
                                                equip(_G.SelectWeapon)
                                            end
                                            spawn(function()
                                                if posrandom <= 1 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,Distance_Farm,50))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=false
                                                elseif posrandom >= 1 and posrandom <= 2 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(50,Distance_Farm,0))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=true
                                                elseif posrandom >= 2 and posrandom <= 3 then
                                                    Tween(v.HumanoidRootPart.CFrame *CFrame.new(0,Distance_Farm,-50))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=false
                                                elseif posrandom >= 3 and posrandom <= 4  then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(-50,Distance_Farm,0))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=true
                                                elseif posrandom >=4 and posrandom <= 5 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
                                                    posrandom = 0
                                                    UesFast=false
                                                end
                                            end)				
                                            if AutoFarmLevel then
                                                if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 150 then
                                                    game:service('VirtualInputManager'):SendKeyEvent(true, "V", false, game)
                                                    game:service('VirtualInputManager'):SendKeyEvent(false, "V", false, game)
											    end
                                            end
                                            busohaki()
                                            v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                            v.Humanoid.JumpPower = 0
                                            v.Humanoid.WalkSpeed = 0
                                            v.HumanoidRootPart.CanCollide = false
                                            if v.Humanoid:FindFirstChild("Animator") then
                                                v.Humanoid.Animator:Destroy()
                                            end
                                            v.Humanoid:ChangeState(11)
                                            sethiddenproperty(ply, "SimulationRadius",  math.huge)
                                        until not AutoFarmLevel or v.Humanoid.Health <= 0
                                    end
                                end
                            elseif game:GetService("ReplicatedStorage"):FindFirstChild("Shanda [Lv. 475]") then
                                Tween(game:GetService("ReplicatedStorage"):FindFirstChild("Shanda [Lv. 475]").HumanoidRootPart.CFrame * CFrame.new(0,20,0))
                            end
                        end
                        )
                    until not (ply.Data.Level.Value >= 30 and ply.Data.Level.Value <= 100) or not AutoFarmLevel or ply.Data.Level.Value >= 100
                else
                    repeat wait()
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894, 5547, -380))
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                    until not AutoFarmLevel or (CFrame.new(-7894, 5547, -380).Position - ply.Character.HumanoidRootPart.Position).Magnitude <= 3500
                end
            else
                if ply.Data.Level.Value <=29 or ply.Data.Level.Value >= 109 then
                pcall(function()
                    CheckQuest()
                    if not string.find(ply.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                        StartMagnet = false
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                    end
                    if ply.PlayerGui.Main.Quest.Visible == false then
                        StartMagnet = false
                        if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - CFrameQuest.Position).Magnitude <= 1200 then
                            TPQuest(CFrameQuest)
                        elseif (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - CFrameQuest.Position).Magnitude >= 1200 then
                            bypasstp(CFrameQuest)
                        end
                        if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - CFrameQuest.Position).Magnitude <= 10 then
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest",QuestName,LevelQuest)
                        end
                    elseif ply.PlayerGui.Main.Quest.Visible == true then
                        if game:GetService("Workspace").Enemies:FindFirstChild(NameMonster) then
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if v.Name == NameMonster and v.Humanoid.Health ~= 0 and v:FindFirstChild("Humanoid") and v:FindFirstChild('HumanoidRootPart') then
                                    if string.find(ply.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                        repeat task.wait()
                                            StartMagnet = true
                                            PosMon = v.HumanoidRootPart.CFrame
                                            if v.Humanoid.Health <= 0 then
                                                unequip(_G.SelectWeapon)
                                            else
                                                equip(_G.SelectWeapon)
                                            end
                                            spawn(function()
                                                if posrandom <= 1 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,Distance_Farm,50))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=false
                                                elseif posrandom >= 1 and posrandom <= 2 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(50,Distance_Farm,0))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=true
                                                elseif posrandom >= 2 and posrandom <= 3 then
                                                    Tween(v.HumanoidRootPart.CFrame *CFrame.new(0,Distance_Farm,-50))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=false
                                                elseif posrandom >= 3 and posrandom <= 4  then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(-50,Distance_Farm,0))
                                                    posrandom = posrandom + 0.1
                                                    UesFast=true
                                                elseif posrandom >=4 and posrandom <= 5 then
                                                    Tween(v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
                                                    posrandom = 0
                                                    UesFast=false
                                                end
                                            end)				
                                            if AutoFarmLevel then
                                                if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 150 then
                                                    game:service('VirtualInputManager'):SendKeyEvent(true, "V", false, game)
                                                    game:service('VirtualInputManager'):SendKeyEvent(false, "V", false, game)
											    end
                                            end
                                            busohaki()
                                            v.HumanoidRootPart.Size=Vector3.new(60,60,60)
                                            v.Humanoid.JumpPower = 0
                                            v.Humanoid.WalkSpeed = 0
                                            v.HumanoidRootPart.CanCollide = false
                                            if v.Humanoid:FindFirstChild("Animator") then
                                                v.Humanoid.Animator:Destroy()
                                            end
                                            v.Humanoid:ChangeState(11)
                                            sethiddenproperty(ply, "SimulationRadius",  math.huge)
                                        until not AutoFarmLevel or v.Humanoid.Health <= 0 or ply.PlayerGui.Main.Quest.Visible == false 
                                    else
                                        StartMagnet = false
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                                    end
                                end
                            end
                        else
                            StartMagnet = false
                            Tween(CFrameMon)
                            if game:GetService("ReplicatedStorage"):FindFirstChild(NameMonster) then
                                Tween(game:GetService("ReplicatedStorage"):FindFirstChild(NameMonster).HumanoidRootPart.CFrame * CFrame.new(0,20,0))
                            end
                        end
                    end
                end
                )
            end
            end
        end
    end
end
)

task.spawn(function()
    while task.wait() do
        pcall(function()
            if AutoFarmLevel then
                if AutoFarmLevel and StartMagnet then
                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                        if InMyNetWork(v.HumanoidRootPart) and v.Name ~= "Greybeard [Lv. 750] [Boss]" and v.Name ~= "Ice Admiral [Lv. 700] [Boss]" and v.Name ~= "Don Swan [Lv. 3000] [Boss]" and v.Name ~= "Saber Expert [Lv. 200] [Boss]" and v.Name ~= "Longma [Lv. 2000] [Boss]" and v.Name ~= "Wysper [Lv. 500] [Boss]"  then
                            v.HumanoidRootPart.CFrame = PosMon
                            v.Humanoid.JumpPower = 0
                            v.Humanoid.WalkSpeed = 0
                            v.HumanoidRootPart.CanCollide = false
                            v.Humanoid:ChangeState(11)
							v.HumanoidRootPart.Size=Vector3.new(60,60,60)
                            sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
                        end
                    end
                end
            end
        end)
    end
end)
spawn(function()
    while wait() do
        if AutoFarmLevel then
            _G.Team = "Pirate"
        end
    end 
end)
spawn(function()
    while task.wait() do
        if game.Players.LocalPlayer.Team == nil then
            pcall(function()
                if _G.Team == "Pirate" then
                    game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.Size = UDim2.new(1000,1000,1000,1000)
                    game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.Position = UDim2.new(-4,0,-5,0)
                    wait(.5)
                    game:GetService("VirtualInputManager"):SendMouseButtonEvent(605,394,0,true,game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton,0)
                    game:GetService("VirtualInputManager"):SendMouseButtonEvent(605,394,0,false,game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton,0)
                end
            end)
        end
    end
end)
