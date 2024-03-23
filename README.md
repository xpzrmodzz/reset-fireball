-- Function to handle player's death
local function forceResetAction()
    local player = game.Players.LocalPlayer
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.Health = 0
    end
end

-- Boucle pour répéter l'action de réinitialisation et d'attaque
while true do
    -- Appeler la fonction de réinitialisation
    forceResetAction()

    -- Boucle pour attaquer le joueur local
    local localPlayer = game:GetService("Players").LocalPlayer -- Récupérer le joueur local

    -- Vérifier si le joueur local a un personnage avec un Humanoid
    if localPlayer.Character and localPlayer.Character:FindFirstChild("Humanoid") then
        local args = {
            [1] = "damage",
            [2] = {
                ["EnemyHumanoid"] = localPlayer.Character.Humanoid
            }
        }
        -- Envoyer l'événement au serveur
        game:GetService("ReplicatedStorage").SkillsInRS.RemoteEvent:FireServer(unpack(args))
    end

    wait(1.5) -- Attendre une courte période entre chaque itération
end
