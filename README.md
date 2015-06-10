
var version="Papa edition";
var checkForUpdate=false;
var updateWindow=false; 
var newUpdate;
var updateMod; 
var ctx = com.mojang.minecraftpe.MainActivity.currentMainActivity.get(); 
 
 function checkVersion() {
    var r  = new java.lang.Runnable() {
        run: function() {
            try {
                var urls= new java.net.URL("https://raw.githubusercontent.com/nono333/DecoBlock-mod-EN-VERSIONS/master/README.md");
                var check = urls.openConnection();
                check.setRequestMethod("GET");
                check.setDoOutput(true);
                check.connect();
                check.getContentLength();
                var script = check.getInputStream();
                var typeb = java.lang.reflect.Array.newInstance(java.lang.Byte.TYPE, 1024);
                var byteCount = 0; 
                var checkedVersion;
                while((byteCount = script.read(typeb)) != -1) { 
                    checkedVersion = new java.lang.String(typeb, 0, byteCount);               
                }
                newUpdate = checkedVersion;
                if(version+"\n" != checkedVersion) {
                    clientMessage(ChatColor.AQUA + "[DBM] " + ChatColor.GREEN +" A new update is out !!");
                    updateWindow=true;
                }
                else if(version+"\n"==checkedVersion){
                clientMessage(ChatColor.AQUA + "[DBM]" + ChatColor.GREEN + " There is no update right now");
                }
            }
            catch(err) {
                clientMessage(ChatColor.AQUA + "[DBM]" + ChatColor.BLUE+ " Internet is " + ChatColor.RED + "offline");
                if(err=="JavaException: java.net.UnknownHostException: raw.githubusercontent.com") {
                      clientMessage(ChatColor.AQUA + "[DBM]" + ChatColor.BLUE+ " Internet is " + ChatColor.RED + "offline");         
                            }
                            else {
                                clientMessage( ChatColor.AQUA + "[DBM]   Error: \n" + err);
                            } 
            }
        }
    }
    var threadt = new java.lang.Thread(r);
    threadt.start();
}
function updateVersion() {
    try {
        var upd = new android.app.AlertDialog.Builder(ctx);
        upd.setTitle("DecoBlock Update Menu");
        upd.setMessage("The mod can be update now !\nDo you want to update it now ?\nCurrent version : " + version + "\nNew version : " + newUpdate + "\nNews Features : ");
        upd.setNegativeButton("No", new android.content.DialogInterface.OnClickListener() {
            onClick: function(par1) {
            dialog.dismiss(); 
   }
        });
        upd.setPositiveButton("Yes", new android.content.DialogInterface.OnClickListener() {
            onClick: function(par1) {
                var ru  = new java.lang.Runnable() {
                    run: function() {
                        try {
                            var urls = new java.net.URL("https://raw.githubusercontent.com/nono333/DecoBlock-mod-EN/master/README.md");
                            var check = urls.openConnection();
                            check.setRequestMethod("GET");
                            check.setDoOutput(true);
                            check.connect();
                            check.getContentLength();
                            var script = check.getInputStream();
                            var typeb = java.lang.reflect.Array.newInstance(java.lang.Byte.TYPE, 1024);
                            var byteCount = 0;
                            while((byteCount = script.read(typeb)) != -1) { 
                                updateMod += new java.lang.String(typeb, 0, byteCount);               
                            }
                            var modpeFolder = ctx.getDir("modscripts", 0);
                            var modpeFile = new java.io.File(modpeFolder, "DecoBlock mod EN.js");
                            var update = new java.io.PrintWriter(modpeFile);
                            update.write(updateMod);
                            update.flush();
                            update.close();
                             
                            try {
                                net.zhuoweizhang.mcpelauncher.ScriptManager.setEnabled(modpeFile, false);
                                net.zhuoweizhang.mcpelauncher.ScriptManager.setEnabled(modpeFile, true);
                                clientMessage(ChatColor.AQUA + "[DBM]" + ChatColor.GREEN + " Succeful Downloading !");
                                   
                            }
                            catch(err) {
                                clientMessage(ChatColor.AQUA + "[DBM] Error: \n" + err);
                            }
                        }
                        catch(err) {
                            clientMessage(ChatColor.AQUA + "[DBM] Error: \n" + err);
                        }
                    }
                }
                var threadt = new java.lang.Thread(ru);
                threadt.start();
            }
        });
        var dialog = upd.create();
        dialog.show() 
    }
    catch(err) {
        clientMessage( ChatColor.AQUA + "[DBM] Error: \n" + err);
    }
}
  
 function modTick(){
 if(checkForUpdate==false) {
        print("Checking for an update");
        ctx.runOnUiThread(new java.lang.Runnable({
            run: function() {
                try {
                    checkVersion();
                }
                catch(err) {
                    clientMessage( ChatColor.AQUA + "[DBM] Error: \n"+err);
                }
            }
        }));
        checkForUpdate=true;
    }
    if(updateWindow) {
        ctx.runOnUiThread(new java.lang.Runnable({
            run: function() {
                try {
                    updateVersion();
                }
                catch(err) {
                  clientMessage( ChatColor.AQUA + "[DBM] Error: \n"+err);  
                }
            }
        }));
        updateWindow=false;
    } 
 } 

function newLevel() {
var redstoneblock = true;
clientMessage(ChatColor.AQUA + "[DBM]" + ChatColor.GREEN + " Hello " + ChatColor.GREEN + getOptionAttr("mp_username"));
clientMessage(ChatColor.AQUA + "[DBM]" + ChatColor.GREEN + " DecoBlock Mod 0.6.2 by nono");
clientMessage(ChatColor.AQUA + "[DBM]" + ChatColor.GREEN + " /Options");
clientMessage(ChatColor.AQUA + "[DBM]" + ChatColor.GREEN + " GRAPHIQUE & DESERT" + ChatColor.RED + " UPDATE");

ModPE.langEdit("tile.stone.stone.name","Polished Stone");

Block.defineBlock(199, "Redstone Fence", [["redstone_block", 0], ["redstone_block", 0], ["redstone_block", 0], ["redstone_block", 0], ["redstone_block", 0], ["redstone_block", 0]], 20, false,11);
 	
Block.defineBlock(200, "Diamond Fence", [["diamond_block", 0], ["diamond_block", 0], ["diamond_block", 0], ["diamond_block", 0], ["diamond_block", 0], ["diamond_block", 0]], 20, false,11);
	
Block.defineBlock(201, "Emerald Fence", [["emerald_block", 0], ["emerald_block", 0], ["emerald_block", 0], ["emerald_block", 0], ["emerald_block", 0], ["emerald_block", 0]], 20, false,11);
Block.defineBlock(206, "Polished Diorite Fence", [["stone", 4], ["stone", 4], ["stone", 4], ["stone", 4], ["stone", 4], ["stone", 4]], 20, false,11);
	
Block.defineBlock(202, "Lapis Lazuli Fence", [["lapis_block", 0], ["lapis_block", 0], ["lapis_block", 0], ["lapis_block", 0], ["lapis_block", 0], ["lapis_block", 0]], 20, false,11);
 		
Block.defineBlock(203, "Iron Fence", [["iron_block", 0], ["iron_block", 0], ["iron_block", 0], ["iron_block", 0], ["iron_block", 0], ["iron_block", 0]], 20, false,11);
	
Block.defineBlock(204, "Coal Fence", [["coal_block", 0], ["coal_block", 0], ["coal_block", 0], ["coal_block", 0], ["coal_block", 0], ["coal_block", 0]], 20, false,11);
	
Block.defineBlock(205, "Golden Fence", [["gold_block", 0], ["gold_block", 0], ["gold_block", 0], ["gold_block", 0], ["gold_block", 0], ["gold_block", 0]], 20, false,11);
Block.defineBlock(207, "Polished Granite Fence", [["stone", 2], ["stone", 2], ["stone", 2], ["stone", 2], ["stone", 2], ["stone", 2]], 20, false,11);
Block.defineBlock(208, "Polished Andesite Fence", [["stone", 6], ["stone", 6], ["stone", 6], ["stone", 6], ["stone", 6], ["stone", 6]], 20, false,11);
Block.defineBlock(209, "Polished Stone Fence", [["stone", 0], ["stone", 0], ["stone", 0], ["stone", 0], ["stone", 0], ["stone", 0]], 20, false,11);
Block.defineBlock(210, "Redstone Slab", [["redstone_block", 0], ["redstone_block", 0], ["redstone_block", 0], ["redstone_block", 0], ["redstone_block", 0], ["redstone_block", 0]], 20, false);
Block.defineBlock(211, "Diamond Slab", [["diamond_block", 0], ["diamond_block", 0], ["diamond_block", 0], ["diamond_block", 0], ["diamond_block", 0], ["diamond_block", 0]],20,  false);
Block.defineBlock(212, "Coal Slab", [["coal_block", 0], ["coal_block", 0], ["coal_block", 0], ["coal_block", 0], ["coal_block", 0], ["coal_block", 0]], 20, false);

Block.defineBlock(213, "Iron Slab", [["iron_block", 0], ["iron_block", 0], ["iron_block", 0], ["iron_block", 0], ["iron_block", 0], ["iron_block", 0]], 20, false);

Block.defineBlock(214, "Lapis Lazuli Slab", [["lapis_block", 0], ["lapis_block", 0], ["lapis_block", 0], ["lapis_block", 0], ["lapis_block", 0], ["lapis_block", 0]], 20, false);

Block.defineBlock(215, "Golden Slab", [["gold_block", 0], ["gold_block", 0], ["gold_block", 0], ["gold_block", 0], ["gold_block", 0], ["gold_block", 0]], 20, false);

Block.defineBlock(216, "Emerald Slab", [["emerald_block", 0], ["emerald_block", 0], ["emerald_block", 0], ["emerald_block", 0], ["emerald_block", 0], ["emerald_block", 0]], 20, false);

Block.defineBlock(217, "Polished Diorite Slab", [["stone", 4], ["stone", 4], ["stone", 4], ["stone", 4], ["stone", 4], ["stone", 4]], 20, false);
Block.defineBlock(218, "Polished Stone Slab", [["stone", 0], ["stone", 0], ["stone", 0], ["stone", 0], ["stone", 0], ["stone", 0]], 20, false);
Block.defineBlock(219, "Polished Granite Slab", [["stone", 2], ["stone", 2], ["stone", 2], ["stone", 2], ["stone", 2], ["stone", 2]], 20, false);
Block.defineBlock(220, "Polished Andesite Slab", [["stone", 6], ["stone", 6], ["stone", 6], ["stone", 6], ["stone", 6], ["stone", 6]], 20, false);
Block.defineBlock(221, "Oak Wood Fence", [["log", 0], ["log", 0], ["log", 0], ["log", 0], ["log", 0], ["log",0 ]], 20, false,11);
Block.defineBlock(222, "Spruce Wood Fence", [["log", 2], ["log", 2], ["log", 2], ["log", 2], ["log", 2], ["log",2 ]], 20, false,11);
Block.defineBlock(223, "Jungle Wood Fence", [["log", 6], ["log", 6], ["log", 6], ["log", 6], ["log", 6], ["log",6 ]], 20, false,11);
Block.defineBlock(224, "Birch Wood Fence", [["log", 4], ["log", 4], ["log", 4], ["log", 4], ["log", 4], ["log",4 ]], 20, false,11);
Block.defineBlock(225, "Acacia Wood Fence", [["log2", 0], ["log2", 0], ["log2", 0], ["log2", 0], ["log2", 0], ["log2",0 ]], 20, false,11);
Block.defineBlock(226, "Dark Oak Wood Fence", [["log2", 2], ["log2", 2], ["log2", 2], ["log2", 2], ["log2", 2], ["log2",2 ]], 20, false,11);
Block.defineBlock(227, "Oak Wood Slab", [["log", 0], ["log", 0], ["log", 0], ["log", 0], ["log", 0], ["log",0 ]], 20, false);
Block.defineBlock(228, "Spruce Wood Slab", [["log", 2], ["log", 2], ["log", 2], ["log", 2], ["log", 2], ["log",2 ]], 20, false);
Block.defineBlock(229, "Birch Wood Slab", [["log", 4], ["log", 4], ["log", 4], ["log", 4], ["log", 4], ["log",4 ]], 20, false);
Block.defineBlock(230, "Jungle Wood Slab", [["log", 6], ["log", 6], ["log", 6], ["log", 6], ["log", 6], ["log",6 ]], 20, false);
Block.defineBlock(231, "Acacia Wood Slab", [["log2", 0], ["log2", 0], ["log2", 0], ["log2", 0], ["log2", 0], ["log2",0 ]], 20, false);
Block.defineBlock(232, "Dark Oak Wood Slab", [["log2", 2], ["log2", 2], ["log2", 2], ["log2", 2], ["log2", 2], ["log2",2 ]], 20, false);
Block.defineBlock(233, "Netherack Fence", [["netherrack", 0], ["netherrack", 0], ["netherrack", 0], ["netherrack", 0], ["netherrack", 0], ["netherrack",0 ]], 20, false,11);
Block.defineBlock(234, "Lava Fence", [["still_lava", 0], ["still_lava", 0], ["still_lava", 0], ["still_lava", 0], ["still_lava", 0], ["still_lava",0 ]], 20, false,11);
Block.defineBlock(235, "Nether Brick Fence", [["nether_brick", 0], ["nether_brick", 0], ["nether_brick", 0], ["nether_brick", 0], ["nether_brick", 0], ["nether_brick",0 ]], 20, false,11);
Block.defineBlock(236, "Netherrack Slab", [["netherrack", 0], ["netherrack", 0], ["netherrack", 0], ["netherrack", 0], ["netherrack", 0], ["netherrack",0 ]], 20, false);
Block.defineBlock(237, "Lava Slab", [["still_lava", 0], ["still_lava", 0], ["still_lava", 0], ["still_lava", 0], ["still_lava", 0], ["still_lava",0 ]], 20, false);
Block.defineBlock(238, "Nether Brick Slab", [["nether_brick", 0], ["nether_brick", 0], ["nether_brick", 0], ["nether_brick", 0], ["nether_brick", 0], ["nether_brick",0 ]], 20, false);
Block.defineBlock(239, "Water Fence", [["still_water", 0], ["still_water", 0], ["still_water", 0], ["still_water", 0], ["still_water", 0], ["still_water",0 ]], 20, false,11);
Block.defineBlock(240, "Snow Fence", [["snow", 0], ["snow", 0], ["snow", 0], ["snow", 0], ["snow", 0], ["snow",0 ]], 20, false,11);
Block.defineBlock(241, "Water Slab", [["still_water", 0], ["still_water", 0], ["still_water", 0], ["still_water", 0], ["still_water", 0], ["still_water",0 ]], 20, false);
Block.defineBlock(242, "Snow Slab", [["snow",0], ["snow", 0], ["snow", 0], ["snow", 0], ["snow", 0], ["snow",0 ]], 20, false);
Block.defineBlock(249, "Ice Fence", [["ice", 0], ["ice", 0], ["ice", 0], ["ice", 0], ["ice", 0], ["ice",0 ]], 20, false,11);
Block.defineBlock(244, "Ice Slab", [["ice", 0], ["ice", 0], ["ice", 0], ["ice", 0], ["ice", 0], ["ice",0 ]], 20, false);
Block.defineBlock(250, "Glowstone Fence", [["glowstone", 0], ["glowstone", 0], ["glowstone", 0], ["glowstone", 0], ["glowstone", 0], ["glowstone",0 ]], 20, false,11);
Block.defineBlock(246, "Glowstone Slab", [["glowstone", 0], ["glowstone", 0], ["glowstone", 0], ["glowstone", 0], ["glowstone", 0], ["glowstone",0 ]], 20, false);
Block.defineBlock(28, "Sand Fence", [["sand", 0], ["sand", 0], ["sand", 0], ["sand", 0], ["sand", 0], ["sand",0 ]], 20, false,11);
Block.defineBlock(29, "Sand Slab", [["sand", 0], ["sand", 0], ["sand", 0], ["sand", 0], ["sand", 0], ["sand",0 ]], 20, false);
Block.defineBlock(33, "Cactus Fence", [["cactus", 0], ["cactus", 0], ["cactus", 0], ["cactus", 0], ["cactus", 0], ["cactus",0 ]], 20, false,11);
Block.defineBlock(34, "Cactus Slab", [["cactus", 0], ["cactus", 0], ["cactus", 0], ["cactus", 0], ["cactus", 0], ["cactus",0 ]], 20, false);
Block.defineBlock(55, "Red Sand Fence", [["sand", 1], ["sand",1], ["sand", 1], ["sand", 1], ["sand", 1], ["sand",1 ]], 20, false,11);
Block.defineBlock(69, "Red Sand Slab", [["sand", 1], ["sand", 1], ["sand", 1], ["sand", 1], ["sand", 1], ["sand",1 ]], 20, false);

Block.setDestroyTime(199, 2);
Block.setDestroyTime(200,2);
Block.setDestroyTime(201,2);
Block.setDestroyTime(202,2);
Block.setDestroyTime(203,2);
Block.setDestroyTime(204,2);
Block.setDestroyTime(205,2);
Block.setDestroyTime(206,2);
Block.setDestroyTime(207,2);
Block.setDestroyTime(208,2);
Block.setDestroyTime(209,2);
Block.setDestroyTime(210,2);
Block.setDestroyTime(211,2);
Block.setDestroyTime(212,2);
Block.setDestroyTime(213,2);
Block.setDestroyTime(214,2);
Block.setDestroyTime(215,2);
Block.setDestroyTime(216,2);
Block.setDestroyTime(217,2);
Block.setDestroyTime(218,2);
Block.setDestroyTime(219,2);
Block.setDestroyTime(220,2);
Block.setDestroyTime(221,2);
Block.setDestroyTime(222,2);
Block.setDestroyTime(223,2);
Block.setDestroyTime(224,2);
Block.setDestroyTime(225,2);
Block.setDestroyTime(226,2);
Block.setDestroyTime(227,2);
Block.setDestroyTime(228,2);
Block.setDestroyTime(229,2);
Block.setDestroyTime(230,2);
Block.setDestroyTime(231,2);
Block.setDestroyTime(232,2);
Block.setDestroyTime(233,2);
Block.setDestroyTime(234,2);
Block.setDestroyTime(235,2);
Block.setDestroyTime(236,2);
Block.setDestroyTime(237,2);
Block.setDestroyTime(238,2);
Block.setDestroyTime(239,2);
Block.setDestroyTime(240,2);
Block.setDestroyTime(241,2);
Block.setDestroyTime(242,2);
Block.setDestroyTime(247,2);
Block.setDestroyTime(244,2);
Block.setDestroyTime(249,2);
Block.setDestroyTime(250,2);
Block.setDestroyTime(246,2);
Block.setDestroyTime(28,2);
Block.setDestroyTime(29,2);
Block.setDestroyTime(33,2);
Block.setDestroyTime(34,2);
Block.setDestroyTime(55,2);
Block.setDestroyTime(69,2);


Player.addItemCreativeInv(199,2);
Player.addItemCreativeInv(200,2);
Player.addItemCreativeInv(201,2);
Player.addItemCreativeInv(202,2);
Player.addItemCreativeInv(203,2);
Player.addItemCreativeInv(204,2);
Player.addItemCreativeInv(205,2);
Player.addItemCreativeInv(206,2);
Player.addItemCreativeInv(207,2);
Player.addItemCreativeInv(208,2);
Player.addItemCreativeInv(209,2);
Player.addItemCreativeInv(210,2);
Player.addItemCreativeInv(211,2);
Player.addItemCreativeInv(212,2);
Player.addItemCreativeInv(213,2);
Player.addItemCreativeInv(214,2);
Player.addItemCreativeInv(215,2);
Player.addItemCreativeInv(216,2);
Player.addItemCreativeInv(217,2);
Player.addItemCreativeInv(218,2);
Player.addItemCreativeInv(219,2);
Player.addItemCreativeInv(220,2);
Player.addItemCreativeInv(221,2);
Player.addItemCreativeInv(222,2);
Player.addItemCreativeInv(223,2);
Player.addItemCreativeInv(224,2);
Player.addItemCreativeInv(225,2);
Player.addItemCreativeInv(226,2);
Player.addItemCreativeInv(227,2);
Player.addItemCreativeInv(228,2);
Player.addItemCreativeInv(229,2);
Player.addItemCreativeInv(230,2);
Player.addItemCreativeInv(231,2);
Player.addItemCreativeInv(232,2);
Player.addItemCreativeInv(233,2);
Player.addItemCreativeInv(234,2);
Player.addItemCreativeInv(235,2);
Player.addItemCreativeInv(236,2);
Player.addItemCreativeInv(237,2);
Player.addItemCreativeInv(238,2);
Player.addItemCreativeInv(239,2);
Player.addItemCreativeInv(240,2);
Player.addItemCreativeInv(241,2);
Player.addItemCreativeInv(242,2);
Player.addItemCreativeInv(247,2);
Player.addItemCreativeInv(244,2);
Player.addItemCreativeInv(249,2);
Player.addItemCreativeInv(250,2);
Player.addItemCreativeInv(246,2);
Player.addItemCreativeInv(28,2);
Player.addItemCreativeInv(29,2);
Player.addItemCreativeInv(33,2);
Player.addItemCreativeInv(34,2);
Player.addItemCreativeInv(55,2);
Player.addItemCreativeInv(69,2);

Block.setShape(210,0,0,0,1,0.5,1);
Block.setShape(211,0,0,0,1,0.5,1);
Block.setShape(212,0,0,0,1,0.5,1);
Block.setShape(213,0,0,0,1,0.5,1);
Block.setShape(214,0,0,0,1,0.5,1);
Block.setShape(215,0,0,0,1,0.5,1);
Block.setShape(216,0,0,0,1,0.5,1);
Block.setShape(217,0,0,0,1,0.5,1);
Block.setShape(218,0,0,0,1,0.5,1);
Block.setShape(219,0,0,0,1,0.5,1);
Block.setShape(220,0,0,0,1,0.5,1);
Block.setShape(227,0,0,0,1,0.5,1);
Block.setShape(228,0,0,0,1,0.5,1);
Block.setShape(229,0,0,0,1,0.5,1);
Block.setShape(230,0,0,0,1,0.5,1);
Block.setShape(231,0,0,0,1,0.5,1);
Block.setShape(232,0,0,0,1,0.5,1);
Block.setShape(236,0,0,0,1,0.5,1);
Block.setShape(237,0,0,0,1,0.5,1);
Block.setShape(238,0,0,0,1,0.5,1);
Block.setShape(241,0,0,0,1,0.5,1);
Block.setShape(242,0,0,0,1,0.5,1);
Block.setShape(244,0,0,0,1,0.5,1);
Block.setShape(246,0,0,0,1,0.5,1);
Block.setShape(29,0,0,0,1,0.5,1);
Block.setShape(34,0,0,0,1,0.5,1);
Block.setShape(69,0,0,0,1,0.5,1);

Item.addCraftRecipe(199,3,0,[0,0,0,0,0,0,0,0,0,0,0,0,280,1,0,331,1,0,280,1,0,280,1,0,331,1,0,280,1,0]);
Item.addCraftRecipe(200,3,0, [0,0,0,280,1,0,264,1,0,280,1,0,280,1,0,264,1,0,280,1,0]);
Item.addCraftRecipe(201,3,0,[0,0,0,280,1,0,388,1,0,280,1,0,280,1,0,388,1,0,280,1,0]);
Item.addCraftRecipe(206,3,0,[0,0,0,280,1,0,1,1,4,280,1,0,280,1,0,1,1,4,280,1,0]);
Item.addCraftRecipe(202,3,0,[0,0,0,280,1,0,351,1,4,280,1,0,280,1,0,351,1,4,280,1,0]);
Item.addCraftRecipe(203,3,0,[0,0,0,280,1,0,265,1,0,280,1,0,280,1,0,265,1,0,280,1,0]);
Item.addCraftRecipe(204,3,0,[0,0,0,280,1,0,263,1,0,280,1,0,280,1,0,263,1,0,280,1,0]);
Item.addCraftRecipe(205,3,0,[0,0,0,280,1,0,266,1,0,280,1,0,280,1,0,266,1,0,280,1,0]);
Item.addCraftRecipe(207,3,0,[0,0,0,280,1,0,1,1,2,280,1,0,280,1,0,1,1,2,280,1,0]);
Item.addCraftRecipe(208,3,0,[0,0,0,280,1,0,1,1,6,280,1,0,280,1,0,1,1,6,280,1,0]);
Item.addCraftRecipe(209,3,0,[0,0,0,280,1,0,1,1,0,280,1,0,280,1,0,1,1,0,280,1,0]);
Item.addCraftRecipe(221,3,0,[0,0,0,280,1,0,17,1,0,280,1,0,280,1,0,17,1,0,280,1,0]);
Item.addCraftRecipe(222,3,0,[0,0,0,280,1,0,17,1,1,280,1,0,280,1,0,17,1,1,280,1,0]);
Item.addCraftRecipe(223,3,0,[0,0,0,280,1,0,17,1,3,280,1,0,280,1,0,17,1,3,280,1,0]);
Item.addCraftRecipe(224,3,0,[0,0,0,280,1,0,17,1,2,280,1,0,280,1,0,17,1,2,280,1,0]);
Item.addCraftRecipe(225,3,0,[0,0,0,280,1,0,162,1,0,280,1,0,280,1,0,162,1,0,280,1,0]);
Item.addCraftRecipe(226,3,0,[0,0,0,280,1,0,162,1,1,280,1,0,280,1,0,162,1,1,280,1,0]);
Item.addCraftRecipe(233,3,0,[0,0,0,280,1,0,87,1,0,280,1,0,280,1,0,87,1,0,280,1,0]);
Item.addCraftRecipe(235,3,0,[0,0,0,280,1,0,405,1,0,280,1,0,280,1,0,405,1,0,280,1,0]);
Item.addCraftRecipe(250,3,0,[0,0,0,280,1,0,348,1,0,280,1,0,280,1,0,348,1,0,280,1,0]);
Item.addCraftRecipe(240,3,0,[0,0,0,280,1,0,80,1,0,280,1,0,280,1,0,80,1,0,280,1,0]);

Item.addShapedRecipe(211, 6, 0, ["   ","ddd","   "], ["d",264,0]);
Item.addShapedRecipe(210, 6, 0, ["   ","ddd","   "], ["d",331,0]);
Item.addShapedRecipe(212, 6, 0, ["   ","ddd","   "], ["d",263,0]);
Item.addShapedRecipe(213, 6, 0, ["   ","ddd","   "], ["d",265,0]);
Item.addShapedRecipe(214, 6, 0, ["   ","ddd","   "], ["d",351,4]);
Item.addShapedRecipe(215, 6, 0, ["   ","ddd","   "], ["d",266,0]);
Item.addShapedRecipe(216, 6, 0, ["   ","ddd","   "], ["d",388,0]);
Item.addShapedRecipe(217, 6, 0, ["   ","ddd","   "], ["d",1,4]);
Item.addShapedRecipe(218, 6, 0, ["   ","ddd","   "], ["d",1,0]);
Item.addShapedRecipe(219, 6, 0, ["   ","ddd","   "], ["d",1,2]);
Item.addShapedRecipe(220, 6, 0, ["   ","ddd","   "], ["d",1,6]);
Item.addShapedRecipe(227, 6, 0, ["   ","ddd","   "], ["d",17,0]);
Item.addShapedRecipe(228, 6, 0, ["   ","ddd","   "], ["d",17,1]);
Item.addShapedRecipe(229, 6, 0, ["   ","ddd","   "], ["d",17,2]);
Item.addShapedRecipe(230, 6, 0, ["   ","ddd","   "], ["d",17,3]);
Item.addShapedRecipe(231, 6, 0, ["   ","ddd","   "], ["d",162,0]);
Item.addShapedRecipe(232, 6, 0, ["   ","ddd","   "], ["d",162,1]);
Item.addShapedRecipe(236, 6, 0, ["   ","ddd","   "], ["d",87,0]);
Item.addShapedRecipe(238, 6, 0, ["   ","ddd","   "], ["d",405,0]);
Item.addShapedRecipe(246, 6, 0, ["   ","ddd","   "], ["d",348,0]);
Item.addShapedRecipe(242, 6, 0, ["   ","ddd","   "], ["d",80,0]);

Block.setLightLevel(250,10);
Block.setLightLevel(210,10);
Block.setLightLevel(199,10);
Block.setLightLevel(234,10);
Block.setLightLevel(237,10);
Block.setLightLevel(246,10);
Block.setLightLevel(250,10);
}


function useItem(x, y, z, itemId, blockId, side){


if(blockId==250){
Level.addParticle(ParticleType.redstone, x, y, z, 1, 0, 0, 2);
Level.addParticle(ParticleType.redstone, x+1, y, z, 1, 1, 0, 2);
Level.addParticle(ParticleType.redstone, x, y, z+1,1,1, 1, 2);
Level.addParticle(ParticleType.redstone, x, y+1, z, 1, 0, 0, 2);
Level.addParticle(ParticleType.redstone, x+1, y+1, z, 1, 1, 0, 2);
Level.addParticle(ParticleType.redstone, x, y+1, z+1,1, 1, 1, 2);

}
if(blockId==199){
Level.addParticle(ParticleType.redstone, x, y, z, 1, 0, 0, 2);
Level.addParticle(ParticleType.redstone, x+1, y, z, 1, 1, 0, 2);
Level.addParticle(ParticleType.redstone, x, y, z+1,1,1, 1, 2);
Level.addParticle(ParticleType.redstone, x, y+1, z, 1, 0, 0, 2);
Level.addParticle(ParticleType.redstone, x+1, y+1, z, 1, 1, 0, 2);
Level.addParticle(ParticleType.redstone, x, y+1, z+1,1, 1, 1, 2);

}
if(blockId==210){
Level.addParticle(ParticleType.redstone, x, y, z, 1, 0, 0, 2);
Level.addParticle(ParticleType.redstone, x+1, y, z, 1, 1, 0, 2);
Level.addParticle(ParticleType.redstone, x, y, z+1,1,1, 1, 2);
Level.addParticle(ParticleType.redstone, x, y+1, z, 1, 0, 0, 2);
Level.addParticle(ParticleType.redstone, x+1, y+1, z, 1, 1, 0, 2);
Level.addParticle(ParticleType.redstone, x, y+1, z+1,1, 1, 1, 2);

}
if(blockId==234){

Level.addParticle(ParticleType.lava, x, y, z, 1, 0, 0, 2);
Level.addParticle(ParticleType.lava, x+1, y, z, 1, 1, 0, 2);
Level.addParticle(ParticleType.lava, x, y, z+1,1,1, 1, 2);
Level.addParticle(ParticleType.lava, x, y+1, z, 1, 0, 0, 2);
Level.addParticle(ParticleType.lava, x+1, y+1, z, 1, 1, 0, 2);
Level.addParticle(ParticleType.lava, x, y+1, z+1,1, 1, 1, 2);
}
if(blockId==237){

Level.addParticle(ParticleType.lava, x, y, z, 1, 0, 0, 2);
Level.addParticle(ParticleType.lava, x+1, y, z, 1, 1, 0, 2);
Level.addParticle(ParticleType.lava, x, y, z+1,1,1, 1, 2);
Level.addParticle(ParticleType.lava, x, y+1, z, 1, 0, 0, 2);
Level.addParticle(ParticleType.lava, x+1, y+1, z, 1, 1, 0, 2);
Level.addParticle(ParticleType.lava, x, y+1, z+1,1, 1, 1, 2);

}
}

function procCmd(command)
{

var cmd = command.split(" ");

if(cmd=="Options")
{
clientMessage(ChatColor.BLUE + "[VERSIONS OPTIONS]" + ChatColor.GREEN + " /VS");
clientMessage(ChatColor.BLUE + "[ADVENCED OPTIONS]" + ChatColor.GREEN + " /ADV");
clientMessage(ChatColor.BLUE + "[CREATOR OPTIONS]" + ChatColor.GREEN + " /C");
}
if (cmd=="C") 
{
clientMessage(ChatColor.BLUE + "[MOD CREATOR]" + ChatColor.GREEN + " nono");
clientMessage(ChatColor.BLUE + "[REPORT BUG METOD]" + ChatColor.GREEN + " nono333mapmod@gmail.com");
clientMessage(ChatColor.BLUE + "[OTHER MOD CREATED]" + ChatColor.GREEN + " /Mod");
}
if (cmd=="Mod")
{
clientMessage(ChatColor.BLUE + "[MOD]" + ChatColor.GREEN + " Mo'Tree Mod");
clientMessage(ChatColor.BLUE + "[MOD]" + ChatColor.GREEN + " Mine Mod");
clientMessage(ChatColor.BLUE + "[MOD]" + ChatColor.GREEN + " COMING SOON");
}
if (cmd=="VS")
{
clientMessage(ChatColor.BLUE + "[0.1.0]" + ChatColor.GREEN + " FIRST UPDATE");
clientMessage(ChatColor.BLUE + "[0.2.0]" + ChatColor.GREEN + " WOOD UPDATE");
clientMessage(ChatColor.BLUE + "[0.3.0]" + ChatColor.GREEN + " HELL UPDATE");
clientMessage(ChatColor.BLUE + "[0.4.0]" + ChatColor.GREEN + " SNOW UPDATE");
clientMessage(ChatColor.BLUE + "[0.5.0]" + ChatColor.GREEN + " GRAPHIQUE & DESERT UPDATE");
}
if (cmd=="ADV")
{

clientMessage(ChatColor.YELLOW + "[DAY]" + ChatColor.GREEN + " /Day");
clientMessage(ChatColor.YELLOW + "[NIGHT]" + ChatColor.GREEN + "/Night"); 
clientMessage(ChatColor.GOLD + "[ITEMS]" + ChatColor.GREEN + " /ItemsFU/WU/HU/SU/GDU (Just for survival)");
clientMessage(ChatColor.GOLD + "[CLEAR]" + ChatColor.GREEN + " /ClearInv (Clear Inventory just for survival)");
}
if (cmd=="ItemsFU")
{
Player.addItemInventory(199,+1,0);
Player.addItemInventory(200,+1,0);
Player.addItemInventory(201,+1,0);
Player.addItemInventory(202,+1,0);
Player.addItemInventory(203,+1,0);
Player.addItemInventory(204,+1,0);
Player.addItemInventory(205,+1,0);
Player.addItemInventory(206,+1,0);
Player.addItemInventory(207,+1,0);
Player.addItemInventory(208,+1,0);
Player.addItemInventory(209,+1,0);
Player.addItemInventory(210,+1,0);
Player.addItemInventory(211,+1,0);
Player.addItemInventory(212,+1,0);
Player.addItemInventory(213+1,0);
Player.addItemInventory(214,+1,0);
Player.addItemInventory(215,+1,0);
Player.addItemInventory(216,+1,0);
Player.addItemInventory(217,+1,0);
Player.addItemInventory(218,+1,0);
Player.addItemInventory(219,+1,0);
Player.addItemInventory(220,+1,0);
clientMessage(ChatColor.GOLD + "[ITEMS]" + ChatColor.GREEN + " You have the Items of the First Update in your inventory");
}
if (cmd=="ItemsWU"){
Player.addItemInventory(221,+1,0);
Player.addItemInventory(222,+1,0);
Player.addItemInventory(223,+1,0);
Player.addItemInventory(224,+1,0);
Player.addItemInventory(225,+1,0);
Player.addItemInventory(226,+1,0);
Player.addItemInventory(227,+1,0);
Player.addItemInventory(228,+1,0);
Player.addItemInventory(229,+1,0);
Player.addItemInventory(230,+1,0);
Player.addItemInventory(231,+1,0);
Player.addItemInventory(232,+1,0);
clientMessage(ChatColor.GOLD + "[ITEMS]" + ChatColor.GREEN + " You have the Items of the Wood Update in your inventory");
}
if (cmd=="ItemsHU"){
Player.addItemInventory(233,+1,0);
Player.addItemInventory(234,+1,0);
Player.addItemInventory(235,+1,0);
Player.addItemInventory(236,+1,0);
Player.addItemInventory(237,+1,0);
Player.addItemInventory(238,+1,0);
Player.addItemInventory(250,+1,0);
Player.addItemInventory(246,+1,0);
clientMessage(ChatColor.GOLD + "[ITEMS]" + ChatColor.GREEN + " You have the Items of the Hell Update in your inventory");
}
if (cmd=="ItemsSU"){
Player.addItemInventory(240,+1,0);
Player.addItemInventory(241,+1,0);
Player.addItemInventory(242,+1,0);
Player.addItemInventory(239,+1,0);
Player.addItemInventory(244,+1,0);
Player.addItemInventory(249,+1,0);
clientMessage(ChatColor.GOLD + "[ITEMS]" + ChatColor.GREEN + " You have the Items of the Snow Update in your inventory");
}
if (cmd=="ItemsGDU"){
Player.addItemInventory(28,+1,0);
Player.addItemInventory(29,+1,0);
Player.addItemInventory(33,+1,0);
Player.addItemInventory(34,+1,0);
Player.addItemInventory(55,+1,0);
Player.addItemInventory(69,+1,0);
clientMessage(ChatColor.GOLD + "[ITEMS]" + ChatColor.GREEN + " You have the Items of the Graphique & Desert Update in your inventory");
}
if (cmd=="ClearInv"){
Player.clearInventorySlot(1);
Player.clearInventorySlot(2);
Player.clearInventorySlot(3);
Player.clearInventorySlot(4);
Player.clearInventorySlot(5);
Player.clearInventorySlot(6);
Player.clearInventorySlot(7);
Player.clearInventorySlot(8);
Player.clearInventorySlot(9);
Player.clearInventorySlot(10);
Player.clearInventorySlot(11);
Player.clearInventorySlot(12);
Player.clearInventorySlot(13);
Player.clearInventorySlot(14);
Player.clearInventorySlot(15);
Player.clearInventorySlot(16);
Player.clearInventorySlot(17);
Player.clearInventorySlot(18);
Player.clearInventorySlot(19);
Player.clearInventorySlot(20);
Player.clearInventorySlot(21);
Player.clearInventorySlot(22);
Player.clearInventorySlot(23);
Player.clearInventorySlot(24);
Player.clearInventorySlot(25);
Player.clearInventorySlot(26);
Player.clearInventorySlot(27);
Player.clearInventorySlot(28);
Player.clearInventorySlot(29);
Player.clearInventorySlot(30);
Player.clearInventorySlot(31);
Player.clearInventorySlot(32);
Player.clearInventorySlot(33);
Player.clearInventorySlot(34);
Player.clearInventorySlot(35);
Player.clearInventorySlot(36);
clientMessage(ChatColor.GOLD + "[CLEAR]" + ChatColor.GREEN + " Inventory Cleared !");
}
if (cmd=="Day"){
Level.setTime(0);
clientMessage(ChatColor.YELLOW + "[DAY]" + ChatColor.GREEN + " Day !");
}
if (cmd=="Night"){
Level.setTime(9999);
clientMessage(ChatColor.YELLOW + "[NIGHT]" + ChatColor.GREEN + " Night !");
}
}


function getOptionAttr(attr){

var sdcard = android.os.Environment.getExternalStorageDirectory();
var mcpeDir = new java.io.File(sdcard.getAbsolutePath(), "games/com.mojang/");
var optionsDir = new java.io.File(mcpeDir, "minecraftpe/");
var optionsFile = new java.io.File(optionsDir, "options.txt");
var br = new java.io.BufferedReader(new java.io.FileReader(optionsFile));
var str, prop;
var ln = new Array();

while((str = br.readLine()) != null){

ln.push(str);

}

i = ln.join().replace(",", ":");
prop = i.split(":");

return prop[prop.indexOf(attr) + 1];

}

