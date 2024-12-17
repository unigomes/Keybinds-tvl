-- Load Rayfield UI Library
local Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/nixckk/UI-Library/refs/heads/main/Rayfield'))()
local Window = Rayfield:CreateWindow({
    Name = "Spell Keybind GUI",
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

-- Tab and Section Configuration
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

-- Spam Toggle and Function for selected spells
local SpamAutem = false
local SpamMenedek = false
local SpamIgnis = false
local SpamMotus = false
local SpamAhShaLana = false
local SpamInvisique = false
local SpamPostTenebras = false
local SpamAscendo = false

-- Function for spamming spells
local function spamSpell(SpellName, SpellCommand)
    local ReplicatedStorage = game:GetService("ReplicatedStorage")
    while true do
        if _G["Spam" .. SpellName] then
            local args = {
                [1] = {
                    ["Incant"] = SpellCommand
                }
            }
            ReplicatedStorage:WaitForChild("RemoteEvents"):WaitForChild("WitchSpell"):FireServer(unpack(args))
        else
            break
        end
        wait(0)
    end
end

-- Create Spam Toggles
GeneralTab:CreateToggle({
    Name = "Spam Autem",
    CurrentValue = false,
    Flag = "SpamAutem",
    Callback = function(Value)
        _G.SpamAutem = Value
        if Value then
            spawn(function() spamSpell("Autem", "autem") end)
        end
    end,
})

GeneralTab:CreateToggle({
    Name = "Spam Menedek",
    CurrentValue = false,
    Flag = "SpamMenedek",
    Callback = function(Value)
        _G.SpamMenedek = Value
        if Value then
            spawn(function() spamSpell("Menedek", "menedek qual surenta") end)
        end
    end,
})

GeneralTab:CreateToggle({
    Name = "Spam Ignis Ubique",
    CurrentValue = false,
    Flag = "SpamIgnis",
    Callback = function(Value)
        _G.SpamIgnis = Value
        if Value then
            spawn(function() spamSpell("IgnisUbique", "ignis ubique") end)
        end
    end,
})

GeneralTab:CreateToggle({
    Name = "Spam Motus",
    CurrentValue = false,
    Flag = "SpamMotus",
    Callback = function(Value)
        _G.SpamMotus = Value
        if Value then
            spawn(function() spamSpell("Motus", "motus") end)
        end
    end,
})

GeneralTab:CreateToggle({
    Name = "Spam Ah Sha Lana",
    CurrentValue = false,
    Flag = "SpamAhShaLana",
    Callback = function(Value)
        _G.SpamAhShaLana = Value
        if Value then
            spawn(function() spamSpell("AhShaLana", "ah sha lana") end)
        end
    end,
})

GeneralTab:CreateToggle({
    Name = "Spam Invisique",
    CurrentValue = false,
    Flag = "SpamInvisique",
    Callback = function(Value)
        _G.SpamInvisique = Value
        if Value then
            spawn(function() spamSpell("Invisique", "invisique") end)
        end
    end,
})

GeneralTab:CreateToggle({
    Name = "Spam Post Tenebras",
    CurrentValue = false,
    Flag = "SpamPostTenebras",
    Callback = function(Value)
        _G.SpamPostTenebras = Value
        if Value then
            spawn(function() spamSpell("PostTenebras", "post tenebras spero lucem") end)
        end
    end,
})

GeneralTab:CreateToggle({
    Name = "Spam Ascendo",
    CurrentValue = false,
    Flag = "SpamAscendo",
    Callback = function(Value)
        _G.SpamAscendo = Value
        if Value then
            spawn(function() spamSpell("Ascendo", "ascendo") end)
        end
    end,
})
