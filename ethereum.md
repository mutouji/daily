#Understanding Ethereum Smart Contract Storage

    contract Storage {
      uint slot 0;  ===> key=0
      mapping(address => uint) slot 1 ===> key = keccak256(address + slot index) ==== address is the key of the map
      struct Entry {
        uint256 id;
        uint256 value;
      }
      Entry c;  // pos2-3
      Entry[] d; // slot 4 for length, uint256(keccak256(slot)) + (index * elementSize) for data

      function Storage() {
        pos0 = 1234;
        pos1[msg.sender] = 5678;
      }
    }
