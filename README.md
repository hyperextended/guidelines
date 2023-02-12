# General guidelines for Hyperextended

## Contributing

### Conventional commits

The use of [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) is strongly encouraged when contributing to any ox or hx resources, they provide a very clear structure for commit titles that assist in organisation and auto-generation of release notes.

The basic structure is as follows:
`<type>[optional scope]: <description>`

E.g.
`feat(client/shops): support for shop peds`
`chore: bump manifest version to v2.22.4`

#### Commit types

- `feat` Commits that add a new feature
- `fix` Commits that fix a bug
- `refactor` Commits that rewrite/restructure your code
- `perf` Commits are special `refactor` commits, that improve performance
- `style` Commits that do not affect the code execution (white-space, formatting, missing semi-colons, etc)
- `tweak` Commits that make small subjective adjustments e.g. changing a colour or wait length
- `chore` Miscellaneous commits e.g. bumping version, removing unused code

#### Scope

Scope is optional, however, it should be included if possible. More than 2 levels deep should be avoided in most cases.

#### Description

Should be informative and to the point, not more than a few words. Additional detail is always welcome and should be added to the comment of the commit.

### Pull requests

Features, refactors and major fixes should first committed to a separate branch or fork before being merged into main. This allows for code review and reduces the number of bugs that make it to main. Small fixes like typos can be committed directly after a sanity check or two.

## Code style

Project Error's repo on this subject is a great starting point ([fivem-lua-style](https://github.com/project-error/fivem-lua-style))

### Code Spacing

Space code out appropriately - separate variable definitions, if statements and loops with a new line if they are at the same indentation level. A few lines can make a remarkable difference to readability.

```lua
-- Bad
lib.callback.register('environment:getInvitees', function(source, groupName)
    local player = Ox.GetPlayer(source)
    local group = GlobalState[('group.%s'):format(groupName)]
    if not player.hasGroup(group.name, group.adminGrade) then return false end
    local invitees = {}
    local playerPos = player.getCoords()
    local players = Ox.GetPlayers()
    local len = #players
    for i = 1, len do
        local nearbyPlayer = players[i]
        if nearbyPlayer.source ~= player.source and not nearbyPlayer.hasGroup(group.name) and #(nearbyPlayer.getCoords() - playerPos) < 10 then
            invitees[#invitees + 1] = {
                name = nearbyPlayer.name,
                id = nearbyPlayer.source
            }
        end
    end
    return invitees
end)

-- Good
lib.callback.register('environment:getInvitees', function(source, groupName)
    local player = Ox.GetPlayer(source)
    local group = GlobalState[('group.%s'):format(groupName)]

    if not player.hasGroup(group.name, group.adminGrade) then return false end

    local invitees = {}
    local playerPos = player.getCoords()
    local players = Ox.GetPlayers()
    local len = #players

    for i = 1, len do
        local nearbyPlayer = players[i]

        if nearbyPlayer.source ~= player.source and not nearbyPlayer.hasGroup(group.name) and #(nearbyPlayer.getCoords() - playerPos) < 10 then
            invitees[#invitees + 1] = {
                name = nearbyPlayer.name,
                id = nearbyPlayer.source
            }
        end
    end

    return invitees
end)
```
