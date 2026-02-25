If the volume is not mounted and changes are made in DB, then on stoping & deleting of container the changes in databses gets deleted.
When we use volume mounting the data is presisted, ther eis two type of volume mounting, named mounting and bind mounting.
In named mounting we define name of the volume and uses it, it gets created in the docker folder while in bind mounting we pass the exact path of where the volume should be
created and stored.
In a named volume:                                                In a bind mount:
-v mysqldata:/var/lib/mysql                                       -v /Users/vanisha/project:/app
mysqldata → volume name                                           Left side is a real folder on your Mac
Docker creates & manages storage automatically                    Docker does NOT manage it
Stored inside Docker’s internal directory                         We control exactly where data lives
On Mac, it lives inside Docker Desktop’s VM storage               Changes reflect immediately
(not directly in your /Users/... folder)
We don’t control the physical path.

In bind mount we are not creating a volume.We are mounting an existing host directory into the container.That’s the subtle difference.
A named volume is managed by Docker and stored in Docker’s internal storage, while a bind mount directly maps a specific host directory into the container. Named volumes are preferred
for persistent production data like databases, whereas bind mounts are mainly used during development for code synchronization.

Default bridge Network (Legacy Behavior)
When Docker was first created containers could communicate using IP, no built-in DNS, name resolution required --link (old feature, now deprecated),Docker kept this behavior for backward compatibility.
So on default bridge:        docker run --name c1 alpine        docker run --name c2 alpine
Inside c1:        ping c2      ❌ Fails
Because there is no DNS service resolving container names.

User-Defined Bridge Network (Modern Behavior)
When you create docker network create mynet. Docker does something extra: It enables an internal DNS server now when containers join this network,docker registers their names.DNS records are
created automatically. Containers can resolve each other by name. So
docker run --network mynet --name c1 alpine      docker run --network mynet --name c2 alpine
Inside c1:  ping c2      Works
Because DNS resolves c2 → container IP.
