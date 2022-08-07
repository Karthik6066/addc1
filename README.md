library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
entity V74X138 is
 Port ( G1,G2A_L,G2B_L : in STD_LOGIC;
 C,B,A : in STD_LOGIC;
 Y_L : out STD_LOGIC_VECTOR (7 downto 0));
end V74X138;
architecture Behavioral of V74X138 is
SIGNAL S,G:STD_LOGIC_VECTOR(2 DOWNTO 0);
SIGNAL Y_LI:STD_LOGIC_VECTOR(7 DOWNTO 0);
begin
S<=C&B&A;
G<=G1&G2A_L&G2B_L;
WITH S SELECT
Y_LI<="11111110" WHEN "000",
"11111101" WHEN "001",
"11111011" WHEN "010",
"11110111" WHEN "011",
"11101111" WHEN "100",
"11011111" WHEN "101",
"10111111" WHEN "110",
"01111111" WHEN "111",
"11111111" WHEN OTHERS;
Y_L<=Y_LI WHEN G="100" ELSE "11111111";
end Behavioral;
SIMULATION RESULT:







library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;
entity V74X148 is
 Port ( EI_L : in STD_LOGIC;
 I_L : in STD_LOGIC_VECTOR (7 downto 0);
 A_L : out STD_LOGIC_VECTOR (2 downto 0);
 GS_L,EO_L : out STD_LOGIC);
end V74X148;
architecture Behavioral of V74X148 is
begin
PROCESS(EI_L,I_L)
VARIABLE J:INTEGER RANGE 7 DOWNTO 0;
VARIABLE A:STD_LOGIC_VECTOR(2 DOWNTO 0);
BEGIN
IF(EI_L='1')THEN A_L<="111";GS_L<='1';EO_L<='1';
ELSE 
FOR J IN 7 DOWNTO 0 LOOP
IF(I_L(J)='0')THEN A:=CONV_STD_LOGIC_VECTOR(J,3);GS_L<='0';EO_L<='1';
A_L<=NOT A;
EXIT;END IF;
END LOOP;
IF(I_L="11111111")THEN A_L<="111";GS_L<='1';EO_L<='0';
END IF;ENDIF;END PROCESS;
end Behavioral;
SIMULATION RESULT:




library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
entity V74X151 is
 Port ( EI_L : in STD_LOGIC;
 C,B,A:IN STD_LOGIC;
D : in STD_LOGIC_VECTOR (7 downto 0);
 Y,Y_L : inout STD_LOGIC);
end V74X151;
architecture Behavioral of V74X151 is
SIGNAL S:STD_LOGIC_VECTOR(2 DOWNTO 0);
SIGNAL YI:STD_LOGIC;
begin
S<=C&B&A;
WITH S SELECT
YI<=D(0)WHEN "000",
D(1)WHEN "001",
D(2)WHEN "010",
D(3)WHEN "011",
D(4)WHEN "100",
D(5)WHEN "101",
D(6)WHEN "110",
D(7)WHEN "111",
'0' WHEN OTHERS;
Y<=YI WHEN EI_L='0' ELSE '0';Y_L<=NOT Y;
end Behavioral;
SIMULATION RESULT:








library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;
entity V74X85 is
 Port ( ALTBIN,AEQBIN,AGTBIN : in STD_LOGIC;
 A,B : in STD_LOGIC_VECTOR (3 downto 0);
 ALTBOUT,AEQBOUT,AGTBOUT : out STD_LOGIC);
end V74X85;
architecture Behavioral of V74X85 is
begin
PROCESS(ALTBIN,AEQBIN,AGTBIN)
BEGIN
IF(A<B) THEN ALTBOUT<='1';AEQBOUT<='0';AGTBOUT<='0';
ELSIF(A>B) THEN ALTBOUT<='0';AEQBOUT<='0';AGTBOUT<='1';
ELSIF(A=B) THEN
IF(ALTBIN='1')THEN ALTBOUT<='1';AEQBOUT<='0';AGTBOUT<='0';
ELSIF(AGTBIN='1')THEN ALTBOUT<='0';AEQBOUT<='0';AGTBOUT<='1';
ELSIF(AEQBIN='1')THEN ALTBOUT<='0';AEQBOUT<='1';AGTBOUT<='0';
END IF; END IF; END PROCESS;
end Behavioral;






library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
entity V74X74 is
 Port ( PRE_L,CLR_L,CLK,D : in STD_LOGIC;
 Q,QB : inout STD_LOGIC);
end V74X74;
architecture Behavioral of V74X74 is
begin
PROCESS(PRE_L,CLR_L,CLK,D)
VARIABLE PC_L:STD_LOGIC_VECTOR(1 DOWNTO 0);
BEGIN
PC_L:=PRE_L&CLR_L;
IF(PC_L="01")THEN Q<='1';QB<='0';
ELSIF(PC_L="10")THEN Q<='0';QB<='1';
ELSIF(PC_L="00")THEN Q<='1';QB<='1';
ELSIF(CLK' EVENT AND CLK='1') THEN Q<= D;QB<=NOT Q;
END IF; END PROCESS;
end Behavioral;




library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
entity V74X109 is
 Port ( PRE_L,CLR_L,CLK,J,KB : in STD_LOGIC;
 Q,QB : inout STD_LOGIC);
end V74X109;
architecture Behavioral of V74X109 is
begin
PROCESS(PRE_L,CLR_L,CLK,J,KB)
VARIABLE PC_L,JKB:STD_LOGIC_VECTOR(1 DOWNTO 0);
BEGIN
PC_L:=PRE_L&CLR_L;JKB:=J&KB;
IF(PC_L="01")THEN Q<='1';QB<='0';
ELSIF(PC_L="10")THEN Q<='0';QB<='1';
ELSIF(PC_L="00")THEN Q<='1';QB<='1';
ELSIF(CLK' EVENT AND CLK='1') THEN 
IF(JKB="01")THEN Q<= Q;QB<= QB;
ELSIF(JKB="00")THEN Q<= '0';QB<='1';
ELSIF(JKB="11")THEN Q<='1';QB<='0';
ELSIF(JKB="10")THEN Q<=NOT Q;QB<=NOT QB;
END IF; END IF;END PROCESS;
end Behavioral;




Program for ones counter

entity vcnt1 is
    Port ( d : in  STD_LOGIC_VECTOR (31 downto 0);
           sum : out  STD_LOGIC_VECTOR (4 downto 0));
end vcnt1;
architecture Behavioral of vcnt1 is
begin
process(d)
variable s:STD_LOGIC_VECTOR(4 downto 0);
begin
s:="00000";
for i in 0 to 31 loop
if d(i)='1' then s:=s+"00001";
end if;
end loop;
sum<=s;
end process;
end Behavioral;




Barrel shifter program

entity rol16 is
    Port ( d : in  STD_LOGIC_VECTOR (15 downto 0);
           s : in  STD_LOGIC_VECTOR (3 downto 0);
           dout : in  STD_LOGIC_VECTOR (15 downto 0));
end rol16;

architecture Behavioral of rol16 is

begin
process(d,s)
variable x,y,z:STD_LOGIC_VECTOR(15 downto 0);
begin
if s(0)='1' then x := d(14 downto 0)&d(15);else x := d;end if;
if s(1)='1' then y := x(13 downto 0)&x(15 downto 14);else y := x;end if;
if s(2)='1' then z := y(11 downto 0)&y(15 downto 12);else z := y;end if;
if s(3)='1' then dout <= z(7 downto 0)&z(15 downto 8);else dout <= z;end if;
end process;
end Behavioral;

