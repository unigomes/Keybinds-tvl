-- Load Rayfield UI Library
local Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/nixckk/UI-Library/refs/heads/main/Rayfield'))()
local Window = Rayfield:CreateWindow({
    Name = "Spell Keybind GUI",
    LoadingTitle = "Loading Spells...",
    LoadingSubtitle = "Customizable",
    DisableRayfieldPrompts = false,
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
local SpamSpellsTab = Window:CreateTab("Spam Spells")
local QetsiyahTab = Window:CreateTab("Qetsiyah Spells")
local HopeTab = Window:CreateTab("Hope Spells")
local DarkJosieTab = Window:CreateTab("Dark Josie Spells")

local GeneralSection = GeneralTab:CreateSection("General Spell Settings")
local SpamSection = SpamSpellsTab:CreateSection("Spam Spell Settings")
local QetsiyahSection = QetsiyahTab:CreateSection("Qetsiyah Spells")
local HopeSection = HopeTab:CreateSection("Hope Spells")
local DarkJosieSection = DarkJosieTab:CreateSection("Dark Josie Spells")

-- General spells for all witches
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

-- Spells that can be spammed
local SpamSpells = {
    { Name = "Autem", DefaultKey = "H", Command = "autem" },
    { Name = "Menedek Qual Surenta", DefaultKey = "I", Command = "menedek qual surenta" },
    { Name = "Ignis Ubique", DefaultKey = "J", Command = "ignis ubique" },
    { Name = "Motus", DefaultKey = "K", Command = "motus" },
    { Name = "Ah Sha Lana", DefaultKey = "L", Command = "ah sha lana" },
    { Name = "Ascendo", DefaultKey = "B", Command = "ascendo" },
}

-- Qetsiyah's exclusive spells
local QetsiyahSpells = {
    { Name = "Ferveret Sanguis", DefaultKey = "J", Command = "ferveret sanguis" },
    { Name = "Ah Sha Lana", DefaultKey = "K", Command = "ah sha lana" },
    { Name = "Corpus Exoquator", DefaultKey = "L", Command = "corpus exoquator" },
    { Name = "Venenum Corpus", DefaultKey = "B", Command = "venenum corpus" },
}

-- Hope's exclusive spells
local HopeSpells = {
    { Name = "Lecutio Maxima", DefaultKey = "J", Command = "lecutio maxima" },
    { Name = "Ventus", DefaultKey = "K", Command = "ventus" },
}

-- Dark Josie's exclusive spells
local DarkJosieSpells = {
    { Name = "Lecutio Maxima", DefaultKey = "J", Command = "lecutio maxima" },
    { Name = "Autem", DefaultKey = "K", Command = "autem" },
    { Name = "Ignis Ubique", DefaultKey = "L", Command = "ignis ubique" },
    { Name = "Ascendo", DefaultKey = "B", Command = "ascendo" },
}

-- Function to create keybinds with a spam toggle for faster casting
local function createKeybinds(tab, spells, section)
    for i, spell in ipairs(spells) do
        local spamState = false  -- Set the spam state off by default
        local keybindButton = tab:CreateKeybind({
            Name = spell.Name,
            CurrentKeybind = spell.DefaultKey,
            HoldToInteract = false,
            Flag = "Keybind" .. i, -- Unique identifier
            Callback = function(Keybind)
                if spamState then
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

        -- Add a toggle to enable/disable the spell spamming
        local toggle = tab:CreateToggle({
            Name = "Spam " .. spell.Name,
            CurrentValue = spamState,  -- Set to OFF by default
            Flag = "SpamToggle" .. i,
            Callback = function(Value)
                spamState = Value  -- Change the state when toggled
                -- Start or stop spam casting
                if Value then
                    -- Start spamming
                    while spamState do
                        local ReplicatedStorage = game:GetService("ReplicatedStorage")
                        local args = {
                            [1] = {
                                ["Incant"] = spell.Command,
                            }
                        }
                        ReplicatedStorage:WaitForChild("RemoteEvents"):WaitForChild("WitchSpell"):FireServer(unpack(args))
                        wait(0)  -- Set a very small delay to spam the spell continuously
                    end
                end
            end,
        })
    end
end

-- Create keybinds for general spells
createKeybinds(GeneralTab, GeneralSpells, GeneralSection)

-- Create spam toggle keybinds for specific spells in Spam Spells tab
createKeybinds(SpamSpellsTab, SpamSpells, SpamSection)

-- Create keybinds for Qetsiyah's exclusive spells
createKeybinds(QetsiyahTab, QetsiyahSpells, QetsiyahSection)

-- Create keybinds for Hope's exclusive spells
createKeybinds(HopeTab, HopeSpells, HopeSection)

-- Create keybinds for Dark Josie's exclusive spells
createKeybinds(DarkJosieTab, DarkJosieSpells, DarkJosieSection)
