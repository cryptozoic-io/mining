# **Super Node Peer Binding**

Super node should submit the peer information from the vcc-app.

## 1.bind the checking node

**Step 1. download and run gvc**

```
./gvc
```

```
./gvc --options you like
```

**Step 2. attach to current gvc from ipc**

```
./gvc attach
```

```
./gvc attach ipc://ipc path of your node .
./gvc attach ipc:/root/vcc/data/gvc
```

**Step 3. add checking node peer to current node**

> enode://49429584f76ec4e85ff14a87db976e0d9770c11777015230b12ee9ece5f6e35f75739c8ac89c7909b4216c29dddc0a143923287d1cdcc283771d1c6bc49e6f68@47.110.143.189:30303

```
admin.addPeer("enode://49429584f76ec4e85ff14a87db976e0d9770c11777015230b12ee9ece5f6e35f75739c8ac89c7909b4216c29dddc0a143923287d1cdcc283771d1c6bc49e6f68@47.110.143.189:30303")
```

Step 4. check the peers

```
admin.peers
```

Check all the peers make sure the checking-node peer exists。

## 2.get the node peer hash and submit

**Step 1.get the node peer information of current node**

```
admin.nodeInfo
```

**Step 2.get the enode information**

the peer informaion is a text begin with enode, full text like this:

> enode://49429584f76ec4e85ff14a87db976e0d9770c11777015230b12ee9ece5f6e35f75739c8ac89c7909b4216c29dddc0a143923287d1cdcc283771d1c6bc49e6f68@47.110.143.189:30303

**Step 3.get the peer hash **

Substring the peer hash from "enode://" to "@....".

For Example:

> enode://49429584f76ec4e85ff14a87db976e0d9770c11777015230b12ee9ece5f6e35f75739c8ac89c7909b4216c29dddc0a143923287d1cdcc283771d1c6bc49e6f68@47.110.143.189:30303

the peer hash is

> 49429584f76ec4e85ff14a87db976e0d9770c11777015230b12ee9ece5f6e35f75739c8ac89c7909b4216c29dddc0a143923287d1cdcc283771d1c6bc49e6f68

**Step 4. submit the peer hash got by step 3**

