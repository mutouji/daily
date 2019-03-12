#Understanding Ethereum Smart Contract Storage

    // h = keccak256
    contract Storage {
        uint a ;                  // slot 0;  ===> key=0
        uint256[2] b;             // slots 1-2;
        struct Entry {
            uint256 id;
            uint256 value;
        }
        Entry c;                  // slot 2-3
        Entry[] d;                // slot 4 for length, uint256(keccak256(slot)) + (index * elementSize) for data

        mapping(uint256 => uint256) e;    // slot 6, data at h(k . 6)
        mapping(uint256 => uint256) f;    // slot 7, data at h(k . 7)

        mapping(uint256 => uint256[]) g;  // slot 8
        mapping(uint256 => uint256)[] h;  // slot 9

        function mapLocation(uint256 slot, uint256 key) public pure returns (uint256) {
            return uint256(keccak256(key, slot));
        }

        function arrLocation(uint256 slot, uint256 index, uint256 elementSize)
        public
        pure
        returns (uint256)
        {
            return uint256(keccak256(slot)) + (index * elementSize);
        }
    }
    
  g[123][0] 如下定位

    // first find arr = g[123]
    arrLoc = mapLocation(8, 123);  // g is at slot 8

    // then find arr[0]
    itemLoc = arrLocation(arrLoc, 0, 1);
