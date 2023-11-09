# mobs_api_cgi
Projet fork depuis https://codeberg.org/tenplus1/mobs_redo pour appliquer correctif


# Correctif
Afin d'éviter un crash du serveur minetest pour un nil value, noua ajoutons une vérification dans le code du fichier api.lua 
L 1113 :

```
function mob_class:is_inside(itemtable)

	local cb = self.object:get_properties().collisionbox
	local pos = self.object:get_pos()

	-- Check if vector module is available
	if vector and vector.offset then
			local nn = minetest.find_nodes_in_area(
					vector.offset(pos, cb[1], cb[2], cb[3]),
					vector.offset(pos, cb[4], cb[5], cb[6]), itemtable)

			if nn and #nn > 0 then
					return true
			end
	else
			return false
	end
end

```
