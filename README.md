-- Contraseña predeterminada
local correctPassword = "555824606"

-- Crear pantalla de inicio de sesión
local LoginScreen = Instance.new("ScreenGui")
local LoginFrame = Instance.new("Frame")
local PasswordBox = Instance.new("TextBox")
local LoginButton = Instance.new("TextButton")
local TitleLabel = Instance.new("TextLabel")
local UICornerLoginFrame = Instance.new("UICorner")

LoginScreen.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

LoginFrame.Parent = LoginScreen
LoginFrame.Size = UDim2.new(0, 400, 0, 200)
LoginFrame.Position = UDim2.new(0.5, -200, 0.5, -100)
LoginFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
LoginFrame.Active = true
LoginFrame.Draggable = true

UICornerLoginFrame.Parent = LoginFrame
UICornerLoginFrame.CornerRadius = UDim.new(0, 18)

TitleLabel.Parent = LoginFrame
TitleLabel.Size = UDim2.new(1, 0, 0, 40)
TitleLabel.Position = UDim2.new(0, 0, 0, 10)
TitleLabel.Text = "Enter Password"
TitleLabel.TextScaled = true
TitleLabel.Font = Enum.Font.GothamBold
TitleLabel.TextColor3 = Color3.fromRGB(240, 240, 240)
TitleLabel.BackgroundTransparency = 1

PasswordBox.Parent = LoginFrame
PasswordBox.Size = UDim2.new(1, -20, 0, 40)
PasswordBox.Position = UDim2.new(0, 10, 0, 60)
PasswordBox.PlaceholderText = "Enter password"
PasswordBox.Font = Enum.Font.Gotham
PasswordBox.TextScaled = true
PasswordBox.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
PasswordBox.TextColor3 = Color3.fromRGB(200, 200, 200)

local UICornerTextBox = Instance.new("UICorner")
UICornerTextBox.Parent = PasswordBox
UICornerTextBox.CornerRadius = UDim.new(0, 12)

LoginButton.Parent = LoginFrame
LoginButton.Size = UDim2.new(1, -20, 0, 50)
LoginButton.Position = UDim2.new(0, 10, 0, 120)
LoginButton.Text = "Login"
LoginButton.TextScaled = true
LoginButton.Font = Enum.Font.GothamBold
LoginButton.BackgroundColor3 = Color3.fromRGB(70, 130, 180)
LoginButton.TextColor3 = Color3.fromRGB(255, 255, 255)

local UICornerLoginButton = Instance.new("UICorner")
UICornerLoginButton.Parent = LoginButton
UICornerLoginButton.CornerRadius = UDim.new(0, 12)

-- Comprobación de la contraseña
LoginButton.MouseButton1Click:Connect(function()
    if PasswordBox.Text == correctPassword then
        -- Si la contraseña es correcta, destruye la pantalla de login y ejecuta la GUI principal
        LoginScreen:Destroy()

        -- Keybinds GUI

        local Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/nixckk/UI-Library/refs/heads/main/Rayfield'))()
        local Window = Rayfield:CreateWindow({
            Name = "Spell Keybind GUI -- Created by Uni",  -- Added the creator's sign next to the title
            LoadingTitle = "Loading Spells...",
            LoadingSubtitle = "Customizable",
            DisableRayfieldPrompts = false,
            SizeX = 1000,  -- Make the GUI wider horizontally to fit multiple tabs
            Theme = {
                Primary = Color3.fromRGB(245, 182, 204), -- Light Pink
                Background = Color3.fromRGB(255, 240, 245),
                Secondary = Color3.fromRGB(225, 156, 176),
                Accent = Color3.fromRGB(250, 200, 218),
                DarkContrast = Color3.fromRGB(215, 170, 186),
                TextColor = Color3.fromRGB(90, 65, 85)
            }
        })

        -- Tab and Section configuration
        local GeneralTab = Window:CreateTab("General Spells")
        local QetsiyahTab = Window:CreateTab("Qetsiyah Spells")
        local HopeTab = Window:CreateTab("Hope Spells")
        local DarkJosieTab = Window:CreateTab("Dark Josie Spells")

        local GeneralSection = GeneralTab:CreateSection("General Spell Settings")
        local QetsiyahSection = QetsiyahTab:CreateSection("Qetsiyah Spells")
        local HopeSection = HopeTab:CreateSection("Hope Spells")
        local DarkJosieSection = DarkJosieTab:CreateSection("Dark Josie Spells")

        -- Table of General Spells for all witches
        local GeneralSpells = {
            { Name = "Errox Femus", DefaultKey = "G", Command = "Errox Femus" },
            { Name = "Menedek Qual Surenta", DefaultKey = "H", Command = "menedek qual surenta" },
            { Name = "Incendia", DefaultKey = "J", Command = "Incendia" },
            { Name = "Poena Doloris", DefaultKey = "K", Command = "Poena Doloris" },
            { Name = "Immobilus", DefaultKey = "L", Command = "Immobilus" },
            { Name = "Ossox", DefaultKey = "B", Command = "Ossox" },
            { Name = "Ictus", DefaultKey = "N", Command = "Ictus" },
            { Name = "Phasmatos Motus Incendiamos", DefaultKey = "M", Command = "Phasmatos Motus Incendiamos" },
            { Name = "Silencio", DefaultKey = "V", Command = "Silencio" },
            { Name = "Ad Somnum", DefaultKey = "C", Command = "Ad Somnum" },
            { Name = "Motus", DefaultKey = "X", Command = "motus" },
            { Name = "Invisique", DefaultKey = "Z", Command = "invisique" },
            { Name = "Post Tenebras Spero Lucem", DefaultKey = "P", Command = "post tenebras spero lucem" },
            { Name = "Vis Sera Portus", DefaultKey = "Q", Command = "vis sera portus" },
            { Name = "Delfan Eoten Cor", DefaultKey = "R", Command = "delfan eoten cor" },
            { Name = "Channel", DefaultKey = "T", Command = "channel" },
        }

        -- Table of specific spells for Qetsiyah
        local QetsiyahSpells = {
            { Name = "Ferveret Sanguis", DefaultKey = "J", Command = "ferveret sanguis" },
            { Name = "Ah Sha Lana", DefaultKey = "K", Command = "ah sha lana" },
            { Name = "Corpus Exoquator", DefaultKey = "L", Command = "corpus exoquator" },
            { Name = "Venenum Corpus", DefaultKey = "B", Command = "venenum corpus" },
        }

        -- Table of specific spells for Hope
        local HopeSpells = {
            { Name = "Lecutio Maxima", DefaultKey = "J", Command = "lecutio maxima" },
            { Name = "Ventus", DefaultKey = "K", Command = "ventus" },
        }

        -- Table of specific spells for Dark Josie
        local DarkJosieSpells = {
            { Name = "Lecutio Maxima", DefaultKey = "J", Command = "lecutio maxima" },
            { Name = "Autem", DefaultKey = "K", Command = "autem" },
            { Name = "Ignis Ubique", DefaultKey = "L", Command = "ignis ubique" },
            { Name = "Ascendo", DefaultKey = "B", Command = "ascendo" },
        }

        -- Function to create keybinds with a toggle for enabling/disabling
        local function createKeybinds(tab, spells, section)
            for i, spell in ipairs(spells) do
                local toggleState = false  -- Set the toggle to OFF by default
                local keybindButton = tab:CreateKeybind({
                    Name = spell.Name,
                    CurrentKeybind = spell.DefaultKey,
                    HoldToInteract = false,
                    Flag = "Keybind" .. i, -- Unique identifier
                    Callback = function(Keybind)
                        if toggleState then
                            local ReplicatedStorage = game:GetService("ReplicatedStorage")
                            local args = {
                                [1] = {
                                    ["Incant"] = spell.Command,
                                }
                            }
                            ReplicatedStorage:WaitForChild("RemoteEvents"):WaitForChild("WitchSpell"):FireServer(unpack(args))
                        end
                    end,
                })

                -- Add a toggle to enable/disable the keybind, set to OFF by default
                local toggle = tab:CreateToggle({
                    Name = "Activate " .. spell.Name,
                    CurrentValue = toggleState,  -- Set to OFF by default
                    Flag = "Toggle" .. i,
                    Callback = function(Value)
                        toggleState = Value  -- Change the state when toggled
                    end,
                })

                -- If the spell requires spamming (Autem, Menedek, etc.), add a Spam toggle
                if spell.Name == "Autem" or spell.Name == "Menedek Qual Surenta" or spell.Name == "Ignis Ubique" or spell.Name == "Motus" or spell.Name == "Ah Sha Lana" or spell.Name == "Invisique" or spell.Name == "Post Tenebras Spero Lucem" or spell.Name == "Ascendo" then
                    tab:CreateToggle({
                        Name = "Spam " .. spell.Name,
                        CurrentValue = false,
                        Flag = "SpamToggle" .. i,
                        Callback = function(Value)
                            _G["Spam" .. spell.Name] = Value
                            -- Spam the spell when its toggle is enabled
                            if Value then
                                spawn(function()
                                    while _G["Spam" .. spell.Name] do
                                        local args = {
                                            [1] = {["Incant"] = spell.Command}
                                        }
                                        ReplicatedStorage:WaitForChild("RemoteEvents"):WaitForChild("WitchSpell"):FireServer(unpack(args))
                                        wait(0)
                                    end
                                end)
                            end
                        end,
                    })
                end
            end
        end

        -- Create keybinds for general spells
        createKeybinds(GeneralTab, GeneralSpells, GeneralSection)

        -- Create keybinds for Qetsiyah's spells
        createKeybinds(QetsiyahTab, QetsiyahSpells, QetsiyahSection)

        -- Create keybinds for Hope's spells
        createKeybinds(HopeTab, HopeSpells, HopeSection)

        -- Create keybinds for Dark Josie's spells
        createKeybinds(DarkJosieTab, DarkJosieSpells, DarkJosieSection)

    else
        print("Incorrect password.")
    end
end)
