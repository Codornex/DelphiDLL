//Declaração explicita da DLL: O sistema carrega a DLL somente quando vai usar e apos usar libera ela da memoria.

(*
O carregamento dinâmico é feito utilizando três API’s do Windows presentes na DLL Kernel32.dll, são elas:
· LoadLibrary: responsável por carregar a DLL para a memória;
· GetProcAddress: recupera o endereço de memória da função que precisamos usar;
· FreeLibrary: elimina da memória a DLL carregada.
*)
unit UnExplicita;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
  Dialogs, Spin, StdCtrls;

//Cria três classes que farão referência as funções em nossa DLL
type
  TMeuUpperCase = function(s: ShortString): ShortString;

  TMeuLowerCase = function(s: ShortString): ShortString;

  TMeuIntToStr = function(Numero: Integer): ShortString;

type
  TForm2 = class(TForm)
    Label1: TLabel;
    edtTexto: TEdit;
    btnMaiusculas: TButton;
    btnMinusculas: TButton;
    Label2: TLabel;
    Label3: TLabel;
    Edit1: TEdit;
    SpinEdit1: TSpinEdit;
    Button1: TButton;
    procedure btnMaiusculasClick(Sender: TObject);
    procedure btnMinusculasClick(Sender: TObject);
    procedure Button1Click(Sender: TObject);
  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  Form2: TForm2;

implementation

{$R *.dfm}

procedure TForm2.btnMaiusculasClick(Sender: TObject);
var
  //Handle receberá a referência da DLL em memória, ou seja, atribuímos a ela o resultado do
  //método LoadLibrary, que é justamente o endereço de memória. Todo programa, quando iniciado(instanciado), recebe um endereço de memória que
  // é a forma como o sistema operacional o mapeia.
  Handle: THandle;

  //A variável mUpperCase por sua vez, receberá o endereço de memória da função MeuUpperCase que está declarada em nossa variável.
  //Isso significa, que poderemos acessar o resultado da função atribuindo-a a um objeto em tela, nesse caso a propriedade Text do Edit2
  mUpperCase: TMeuUpperCase;
begin
  Handle := LoadLibrary('MinhaDll.dll');
  if Handle <> 0 then
  begin
    mUpperCase := GetProcAddress(Handle, 'MeuUpperCase');
    edtTexto.Text := mUpperCase(edtTexto.Text);
    FreeLibrary(Handle); //Libera DLL da memoria
  end
  else
    ShowMessage('Não foi possível carregar a DLL.');  
end;

procedure TForm2.btnMinusculasClick(Sender: TObject);
var
  Handle: THandle;
  mLowerCase: TMeuLowerCase;
begin
  Handle := LoadLibrary('MinhaDll.dll');
  if Handle <> 0 then
  begin
    mLowerCase := GetProcAddress(Handle, 'MeuLowerCase');
    edtTexto.Text := mLowerCase(edtTexto.Text);
    FreeLibrary(Handle);
  end
  else
    ShowMessage('Não foi possível carregar a DLL.');  
end;

procedure TForm2.Button1Click(Sender: TObject);
var
  Handle: THandle;
  mIntToStr: TMeuIntToStr;
begin
  Handle := LoadLibrary('MinhaDll.dll');
  if Handle <> 0 then
  begin
    mIntToStr := GetProcAddress(Handle, 'MeuIntToStr');
    Edit1.Text := mIntToStr(SpinEdit1.Value);
    FreeLibrary(Handle);
  end
  else
    ShowMessage('Não foi possível carregar a DLL.');
end;

end.

