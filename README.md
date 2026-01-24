flowchart LR
    %% External
    Internet((Internet))
    Clients[LAN / VPN Clients]

    %% Caddy network
    subgraph caddy_net["caddy (reverse-proxy network)"]
        Caddy[Caddy Reverse Proxy]
    end

    %% arr network
    subgraph arr_net["arr-network"]
        Radarr[Radarr]
        Prowlarr[Prowlarr]
        Transmission[Transmission<br/>(OpenVPN)]
        Jellyfin[Jellyfin]
    end

    %% vpn network
    subgraph vpn_net["vpn-network"]
        WireGuard[WireGuard<br/>(wg-easy)]
        AdGuard[AdGuard Home]
    end

    %% Traffic flow
    Internet --> Caddy
    Clients --> Caddy

    %% Explicit network attachments
    Caddy --> Jellyfin
    Caddy --> Radarr
    Caddy --> Prowlarr

    %% VPN & DNS flow
    WireGuard --> AdGuard
    Clients --> WireGuard
