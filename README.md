### Info
Reads the cluster logs and sends a message to discord about the administrator login 
and the cheat commands used

### Setup
Need Python 3.10 or later
Need requests package "pip install requests"

### Config
    #Set discord webhook URL
    webhook_url = "https://discord.com/api/webhooks/1214978965471756418/Ln6OXfl44444444444rrrrrrrrrtttttttttttt"
    
    #Set admins SteamIDs
    id_list = ['PostLogin Account: 76561191111111111', 'PostLogin Account: 76561192222222222', 'ServerCheat_Implementation']
    
    #Set full path to logs
    log_files = [
        'C:/moe_cluster/moe/MOE/Saved/Logs/SceneServer_1000.log',
        'C:/moe_cluster/moe/MOE/Saved/Logs/SceneServer_2000.log',
        'C:/moe_cluster/moe/MOE/Saved/Logs/SceneServer_3000.log'
    ]
    
    #Set match the server name and log file
    log_files_dict = {
        'SceneServer_1000.log': 'Кластер: PVE1',
        'SceneServer_2000.log': 'Кластер: PVP',
        'SceneServer_3000.log': 'Кластер: PVE2'
    }


### Donate for me
https://yoomoney.ru/to/4100116619431314
#
https://fkwallet.io  ID: F7202415841873335
