-- Tenta forçar todos os estilos como desbloqueados no lado do cliente
-- Use no F9 no Roblox, ou em um LocalScript

local player = game.Players.LocalPlayer

-- Procura pastas e valores que tenham relação com estilos
local function unlockAllStyles()
    -- Procura as pastas/valores comuns: Styles, Estilos, StylesFolder
    for _, folderName in ipairs({"Styles", "Estilos", "StylesFolder"}) do
        local stylesFolder = player:FindFirstChild(folderName)
        if stylesFolder then
            for _, child in ipairs(stylesFolder:GetChildren()) do
                if child:IsA("BoolValue") or child:IsA("IntValue") then
                    child.Value = true -- BoolValue normal
                end
            end
            print("[+] Todos os estilos em", folderName, "foram ativados/localmente.")
        end
    end

    -- Algum jogo pode usar strings/atributos no Player
    for _, attr in ipairs(player:GetAttributes()) do
        if tostring(attr):lower():match("style") then
            player:SetAttribute(attr, true)
        end
    end

    -- Pode tentar modificar GUIs localmente também
    for _, gui in ipairs(player.PlayerGui:GetDescendants()) do
        if gui:IsA("TextLabel") and gui.Text:lower():match("bloqueado") then
            gui.Text = "DESBLOQUEADO"
            gui.TextColor3 = Color3.new(0,1,0)
        end
    end
end

unlockAllStyles()
