pragma solidity >=0.4.24 <0.7.0;
contract MaterialProvider2 {
    struct Mats {
        uint id;
        int aluminum_bars;
        int stainless_steel_sheets;
        int springs;
        int bumper_rubber_bands;
        int interior_light_bulbs;
        int display_leds_panels;
        
    }
    Mats[] public mats;
    uint public nextId = 1;
    function create(int floor, int elevator) public {
        int aluminum_bars;
        int stainless_steel_sheets;
        int springs;
        int bumper_rubber_bands;
        int interior_light_bulbs;
        int display_leds_panels;
        aluminum_bars = 100 * elevator;
        stainless_steel_sheets = 40 * elevator;
        springs = 50 * elevator;
        bumper_rubber_bands = 100 * elevator;
        interior_light_bulbs = 5 * elevator;
        display_leds_panels = 2 * elevator;
        mats.push(Mats(nextId, aluminum_bars, stainless_steel_sheets, springs, bumper_rubber_bands, interior_light_bulbs, display_leds_panels));
        nextId++;
    }
    function find(uint id) internal view returns(uint){
        for(uint i = 0; i < mats.length ; i++){
            if(mats[i].id == id){
                return i;
            }
        }
        revert ('Order does not exist');
    }
      function read(uint id) public view returns(uint, int, int, int, int, int, int){
        uint i = find(id);
        return(mats[i].id, mats[i].aluminum_bars, mats[i].stainless_steel_sheets, mats[i].springs, mats[i].bumper_rubber_bands, mats[i].interior_light_bulbs, 
        mats[i].display_leds_panels);
    }
      function destroy(uint id) public {
        uint i = find(id);
        delete mats[i];
    }
}
