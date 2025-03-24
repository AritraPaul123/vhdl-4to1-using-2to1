library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity MUX4to1 is
    Port ( A   : in  STD_LOGIC;
           B   : in  STD_LOGIC;
           C   : in  STD_LOGIC;
           D   : in  STD_LOGIC;
           Sel : in  STD_LOGIC_VECTOR(1 downto 0);
           Y   : out STD_LOGIC);
end MUX4to1;

architecture Structural of MUX4to1 is

    --Component Declaration for 2:1 MUX
    component MUX2to1
        Port ( A   : in  STD_LOGIC;
               B   : in  STD_LOGIC;
               Sel : in  STD_LOGIC;
               Y   : out STD_LOGIC);
    end component;

    -- Signals for intermediate MUX outputs
    
    signal MUX1_out, MUX2_out : STD_LOGIC;

begin

    -- First level of 2:1 MUXes
    
    MUX1: MUX2to1 port map (A => A, B => B, Sel => Sel(0), Y => MUX1_out);
    MUX2: MUX2to1 port map (A => C, B => D, Sel => Sel(0), Y => MUX2_out);

    -- Second level of 2:1 MUX
    
    MUX3: MUX2to1 port map (A => MUX1_out, B => MUX2_out, Sel => Sel(1), Y => Y);

end Structural;
