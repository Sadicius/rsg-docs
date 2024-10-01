---
description: Keep track of your vitals in style
---

# ℹ rsg-hud

## Introduction

* Player heads-up display that tracks vital information such as health, armor, food level, thirst level, etc.

{% hint style="info" %}
The settings menu uses keymapping and is defaulted to "I"
{% endhint %}

{% hint style="danger" %}
Player settings are stored using KVP which is located on the player's machine so the only way to reset them is by using the in-game menu buttons
{% endhint %}

## FAQ&#x20;

## Useful events

### hud:server:GainStress

* Source code for reference

```etlua
RegisterNetEvent('hud:server:GainStress', function(amount)
    local src = source
    local Player = RSGCore.Functions.GetPlayer(src)
    local newStress
    if not Player or (Config.DisablePoliceStress and Player.PlayerData.job.name == 'police') then return end
    if not ResetStress then
        if not Player.PlayerData.metadata['stress'] then
            Player.PlayerData.metadata['stress'] = 0
        end
        newStress = Player.PlayerData.metadata['stress'] + amount
        if newStress <= 0 then newStress = 0 end
    else
        newStress = 0
    end
    if newStress > 100 then
        newStress = 100
    end
    Player.Functions.SetMetaData('stress', newStress)
    TriggerClientEvent('hud:client:UpdateStress', src, newStress)
    TriggerClientEvent('RSGCore:Notify', src, Lang:t("notify.stress_gain"), 'error', 1500)
end)
```

* How to use

```etlua
TriggerServerEvent('hud:server:GainStress', --[[number]])) 
OR
TriggerServerEvent('hud:server:GainStress', math.random(1, 3))
```

{% hint style="info" %}
If you trigger this client side you don't need to define source
{% endhint %}

### hud:server:RelieveStress

* Source code for reference

```etlua
RegisterNetEvent('hud:server:RelieveStress', function(amount)
    local src = source
    local Player = RSGCore.Functions.GetPlayer(src)
    local newStress
    if not Player then return end
    if not ResetStress then
        if not Player.PlayerData.metadata['stress'] then
            Player.PlayerData.metadata['stress'] = 0
        end
        newStress = Player.PlayerData.metadata['stress'] - amount
        if newStress <= 0 then newStress = 0 end
    else
        newStress = 0
    end
    if newStress > 100 then
        newStress = 100
    end
    Player.Functions.SetMetaData('stress', newStress)
    TriggerClientEvent('hud:client:UpdateStress', src, newStress)
    TriggerClientEvent('RSGCore:Notify', src, Lang:t("notify.stress_removed"))
end)
```

* How to use

```etlua
TriggerServerEvent('hud:server:RelieveStress', --[[number]])) 
OR
TriggerServerEvent('hud:server:RelieveStress', math.random(1, 3))
```